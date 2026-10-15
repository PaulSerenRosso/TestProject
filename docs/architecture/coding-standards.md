# Coding Standards

Status: Active, rewritten 2026-10-15 for Solo Tutor (previous Lab Kit version: git history, commit `4e151cf`). Wins over personal preference of any developer agent; the PM spec and tech-spec win over this file. Deviation: see `dev-workflow.md` section 7.
Goal: the whole code base looks written by one hand, readable by a portfolio reviewer. Project prefix `Tutor` is an ASSUMPTION (overview Q3); if it changes, rename here first.

## 1. Naming

| Thing | Rule | Example |
|---|---|---|
| Types, methods, properties, events | PascalCase | `ExerciseSpecValidator`, `Check`, `AttemptRecorded` |
| Interfaces | `I` + PascalCase | `IExerciseComposer` |
| Private/protected fields | `_camelCase` | `_catalog` |
| Locals, parameters | camelCase | `targetVolumeMl` |
| Constants, static readonly | PascalCase | `MaxRepairAttempts` |
| Unit-bearing members | unit suffix | `VolumeMl`, `ConcentrationGPerL`, `DurationMs` |
| Files | one top-level type per file, file name = type name | `DilutionFamily.cs` |
| Folders | PascalCase, grouped by feature inside an assembly folder | `Core/Exercises/Families/` |
| Assemblies | `Tutor.<Layer>`; folder name = layer | `Tutor.Core` |
| Namespaces | = assembly name plus feature folder | `Tutor.Core.Exercises` |
| Server projects | `Tutor.Server`, `Tutor.Server.Tests`, `Tutor.Core.Shared`, `Tutor.Core.Tests` | |
| Scenes | `<Build>_<Name>` | `Web_Main`, `Quest_Main`, `Lab_Bench` |
| Prefabs | PascalCase, size/variant suffix after `_` | `Beaker_250ml` |
| Materials | `M_` prefix | `M_GlassClear` |
| ScriptableObject assets | PascalCase noun | `PresentationCatalog` |
| JSON data files | kebab-case | `bricks.json`, `facts.json` |
| Tests | class `<Type>Tests`; method `Method_Condition_Expected` | `Check_SwappedRatio_ReturnsTag` |
| Content ids (skills, bricks, facts, families) | lowercase kebab-case strings | `dilution`, `f-dilution-conservation` |
| Error tags | lowercase kebab-case | `unit-ml-l`, `swapped-ratio` |

## 2. C# style
- Target the C# version of the installed Unity; **`Core` must also compile under the server's pinned `LangVersion`** (same version, overview section 5). No preview features.
- 4 spaces, Allman braces, always braces on `if`/`for`. Max line about 120.
- `var` only when the type is obvious on the right side.
- One `using` block at top, sorted, no unused. File-scoped namespaces are not used (Unity-wide consistency): `namespace X { }`.
- Expression-bodied members for one-liners only.
- `sealed` on classes not designed for inheritance. `readonly` where possible. Prefer `IReadOnlyList<T>` on public APIs.
- No `dynamic`, no reflection in gameplay code, no `#region`.
- Public Core API gets an XML `<summary>`; everything else is self-describing (section 9).

## 3. Layer rules (enforced by asmdefs and by the server build)
See `architecture-overview.md` section 5. `Core` must not use `UnityEngine`, `Debug`, `Time`, `System.Random`, `DateTime.Now`, threads, files or network. It is compiled by Unity **and** by `server/Tutor.Core.Shared`; if you need one of these in Core, you are in the wrong layer. Randomness comes from `Pcg32`, time from a value passed in.

## 4. MonoBehaviour vs plain C#
- Logic lives in plain C# classes (`Core`, or plain classes in other assemblies). A MonoBehaviour is a **thin adapter**: serialized references, lifecycle, forwarding to plain objects, rendering.
- A MonoBehaviour over about 150 lines or with branching game logic is a smell: extract a plain class.
- No static mutable state, no singletons. Dependencies come through constructors or `Init(...)` (ADR-010).

## 5. Serialization and Inspector
- `[SerializeField] private` for Inspector fields; never `public` fields for wiring. Add `[Tooltip]` only when units or meaning are not obvious.
- Validate serialized references once in `Awake`: if null, `Debug.LogError` naming the object, and disable the component.
- Magic numbers become serialized fields or content data. Tunable values (ranges, difficulty bands, credit costs) never live in code.

## 6. Events and communication
- Logic to presentation: C# events (`event Action<...>`) raised by plain classes. Subscribe in `OnEnable`, unsubscribe in `OnDisable`. Never use `SendMessage`, `UnityEvent` for code-to-code wiring, or global event buses.
- Player intent to logic: construct a `StudentAction` or an answer and call the session/family API.
- Request/response: `async` method returning a result (section 8).

## 7. ScriptableObjects
Only for presentation mapping (`Data/Presentation/`): content id to prefab, color, icon. They hold data, never runtime state. Domain data is JSON (ADR-011).

## 8. Async, coroutines, and WebGL (ADR-008)
- Network work: `async` methods or `Awaitable` over `UnityWebRequest`, returning result objects. Coroutines only for short presentation sequences (a pour animation, a fade).
- **Forbidden in every assembly that can run in WebGL (`Core`, `Net`, `Lab`, `Web`, and shared code in `Quest`):** `Thread`, `ThreadPool`, `Task.Run`, `Task.ContinueWith`, `ConfigureAwait(false)`, `Task.Delay`, `System.Threading.Timer`, `CancellationTokenSource` with a timeout, `System.Net` sockets/`HttpClient`, async `FileStream`. Use `UnityWebRequest` timeouts and frame-based waits.
- No `async void` except Unity event handlers, which must `try/catch` and log. No third-party async library (UniTask etc.).
- Server code (`Tutor.Server`) uses normal ASP.NET Core async/await with `CancellationToken`; the restrictions above apply only to code shared with Unity.

## 9. Errors, logging, comments
- Expected failures (invalid spec, refused request, quota, network error) are **values**: return `Result<T>`-style objects with a list of `Diagnostic { Code, Message, Path }`. No exceptions for control flow.
- Exceptions only for programmer errors (`ArgumentNullException` on public Core entry points, impossible states).
- `Core` does not log. Unity layers log with `Debug.Log/LogWarning/LogError` and a short prefix `[Web]`, `[Quest]`, `[Net]`, `[Lab]`. Pass the context object as the second argument when one exists. No log spam in `Update`.
- Server logging uses `ILogger`; **never log student questions, AI prompts/answers, passwords or tokens** (ADR-006).
- User-visible errors are shown in the UI, not only in the console.
- Comments explain **why**, never what. No commented-out code. TODOs carry the story ID: `// TODO(S2.1): ...`.

## 10. GC and performance (Quest and WebGL)
- No allocations in `Update`, `FixedUpdate`, or per-frame paths: no `new` of reference types, no LINQ, no string concatenation, no boxing. Reuse lists (`Clear()`). (Exercise generation and validation run on demand, not per frame; they may allocate.)
- No `GetComponent`, `Find*`, `Camera.main` per frame; cache in `Awake`/`Init`.
- Particle counts and lights are budgeted per scene (measured in SP-4/SP-5). Quest scenes: mobile URP settings, no real-time shadows unless measured. WebGL: watch build size and load time.

## 11. Security and data
- Never commit secrets (ADR-009). Config keys are read from environment or gitignored local files.
- Treat every downloaded or AI-produced JSON as untrusted: validate with `Core` before use (client and server).
- Never use `TypeNameHandling` in Newtonsoft.
- Store no real personal data and no chat text (ADR-006).
- Server endpoints: validate size and shape of every request, check the quota before any AI call, return generic errors to clients.

## 12. Unity do and don't
| Do | Don't |
|---|---|
| Keep `.meta` files committed; create/move/rename assets via Unity (CLI), never by hand | Hand-edit `.meta`, `.unity`, `.prefab` files |
| One scene bootstrap as composition root | `DontDestroyOnLoad` singletons |
| Prefer prefab variants over duplicates | Deep nested prefab overrides |
| Use `TryGetComponent` when absence is valid | `GetComponent` followed by unchecked use |
| Input through the Input System / OpenXR actions | `UnityEngine.Input` legacy, device-specific code |
| Layer/tag names as constants | String literals scattered in code |

## 13. Canonical templates

Plain C# class (Core):
```csharp
namespace Tutor.Core.Validation
{
    /// <summary>Checks an exercise spec against the content and returns all problems found.</summary>
    public sealed class ExerciseSpecValidator
    {
        private readonly ContentCatalog _content;

        public ExerciseSpecValidator(ContentCatalog content)
        {
            _content = content ?? throw new ArgumentNullException(nameof(content));
        }

        public ValidationResult Validate(ExerciseSpec spec)
        {
            var result = new ValidationResult();
            if (!_content.HasFamily(spec.Family))
            {
                result.Add("unknown-family", $"Unknown family '{spec.Family}'.", "family");
            }
            return result;
        }
    }
}
```

Thin MonoBehaviour adapter:
```csharp
namespace Tutor.Lab
{
    public sealed class GlassView : MonoBehaviour
    {
        [SerializeField] private Renderer _liquidRenderer;

        private BenchState _state;
        private string _glassId;

        public void Init(BenchState state, string glassId)
        {
            _state = state;
            _glassId = glassId;
        }

        private void Awake()
        {
            if (_liquidRenderer == null)
            {
                Debug.LogError($"[Lab] {name}: _liquidRenderer is not assigned.", this);
                enabled = false;
            }
        }

        private void OnEnable()  { if (_state != null) _state.Changed += OnStateChanged; }
        private void OnDisable() { if (_state != null) _state.Changed -= OnStateChanged; }

        private void OnStateChanged() { /* update visuals only; no exercise logic */ }
    }
}
```

Test:
```csharp
[Test]
public void Validate_UnknownFamily_ReturnsDiagnostic()
{
    var validator = new ExerciseSpecValidator(TestContent.Minimal());
    var result = validator.Validate(TestSpecs.WithFamily("nope"));
    Assert.That(result.Has("unknown-family"), Is.True);
}
```
Note: `Init` is called before `OnEnable` only if the object is created inactive or the bootstrap calls it before enabling; the tech-spec of a view must state the order. Core tests use NUnit only (no Unity assertions) so `dotnet test` can run them (ADR-012).

Server endpoint (minimal API, ASP.NET Core):
```csharp
app.MapPost("/attempts", async (AttemptRequest request, ClaimsPrincipal user, AttemptService attempts, CancellationToken ct) =>
{
    var outcome = await attempts.RecordAsync(user.GetStudentId(), request, ct);
    return outcome.IsValid ? Results.Ok(outcome.Value) : Results.BadRequest(outcome.ToError());
}).RequireAuthorization();
```
Endpoints stay thin: parse, call a service, map the result. Logic lives in services or `Core`.

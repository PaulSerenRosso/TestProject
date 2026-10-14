# Coding Standards

Status: Active, 2026-10-14. Wins over personal preference of any developer agent; the PM spec and tech-spec win over this file. Deviation: see `dev-workflow.md` section 7.
Goal: the whole code base looks written by one hand, readable by a portfolio reviewer.

## 1. Naming

| Thing | Rule | Example |
|---|---|---|
| Types, methods, properties, events | PascalCase | `ExperimentVerifier`, `Apply`, `EventRaised` |
| Interfaces | `I` + PascalCase | `IExperimentAuthor` |
| Private/protected fields | `_camelCase` | `_rules` |
| Locals, parameters | camelCase | `amountMl` |
| Constants, static readonly | PascalCase | `MaxRepairAttempts` |
| Unit-bearing members | unit suffix | `VolumeMl`, `TemperatureC`, `RateMlPerS` |
| Files | one top-level type per file, file name = type name | `Simulation.cs` |
| Folders | PascalCase, grouped by feature inside an assembly folder | `Core/Simulation/Rules/` |
| Assemblies | `LabKit.<Layer>`; folder name = layer | `LabKit.Core` |
| Namespaces | = assembly name plus feature folder | `LabKit.Core.Simulation` |
| Scenes | `<Build>_<Name>` | `Authoring_Main`, `Lab_Sandbox`, `Quest_Main` |
| Prefabs | PascalCase, size/variant suffix after `_` | `Beaker_250ml` |
| Materials | `M_` prefix | `M_GlassClear` |
| ScriptableObject assets | PascalCase noun | `PresentationCatalog` |
| JSON data files | kebab-case | `substances.json`, `exp-0001.json` |
| Tests | class `<Type>Tests`; method `Method_Condition_Expected` | `Pour_EmptySource_ReturnsError` |
| Catalog / experiment IDs | lowercase kebab-case strings | `water`, `beaker-250` |

## 2. C# style
- Target the C# version of the installed Unity; no preview features.
- 4 spaces, Allman braces, always braces on `if`/`for`. Max line about 120.
- `var` only when the type is obvious on the right side.
- One `using` block at top, sorted, no unused. File-scoped namespaces are not used (keep Unity-wide consistency): `namespace X { }`.
- Expression-bodied members for one-liners only.
- `sealed` on classes not designed for inheritance. `readonly` where possible. Prefer `IReadOnlyList<T>` on public APIs.
- No `dynamic`, no reflection in gameplay code, no `#region`.
- Public Core API gets an XML `<summary>`; everything else is self-describing (section 9).

## 3. Layer rules (enforced by asmdefs)
See `architecture-overview.md` section 4. `Core` must not use `UnityEngine`, `Debug`, `Time`, `Random`, `DateTime.Now`, files or network. If you need one of them in Core, you are in the wrong layer.

## 4. MonoBehaviour vs plain C#
- Logic lives in plain C# classes (`Core`, or plain classes in other assemblies). A MonoBehaviour is a **thin adapter**: serialized references, lifecycle, forwarding to plain objects, rendering.
- A MonoBehaviour over about 150 lines or with branching game logic is a smell: extract a plain class.
- No static mutable state, no singletons. Dependencies come through constructors or `Init(...)` (ADR-007).

## 5. Serialization and Inspector
- `[SerializeField] private` for Inspector fields; never `public` fields for wiring. Add `[Tooltip]` only when units or meaning are not obvious.
- Validate serialized references once in `Awake`: if null, `Debug.LogError` naming the object, and disable the component.
- Magic numbers become serialized fields or catalog data. Tunable gameplay values never live in code.

## 6. Events and communication
- Simulation to presentation: C# events (`event Action<SimEvent>`) raised by plain classes. Subscribe in `OnEnable`, unsubscribe in `OnDisable`. Never use `SendMessage`, `UnityEvent` for code-to-code wiring, or global event buses.
- Player intent to simulation: construct a `LabAction` and call `Simulation.Apply`.
- Request/response: `async` method returning a result (section 8).

## 7. ScriptableObjects
Only for presentation mapping (`Data/Presentation/`): catalog ID to prefab, color, VFX. They hold data, never runtime state. Domain data is JSON (ADR-008).

## 8. Async and coroutines
- Network and file work: `async Task`/`Awaitable` with a `CancellationToken`; callers handle cancellation. No `async void` except Unity event handlers, which must `try/catch` and log.
- Coroutines only for short presentation sequences (a pour animation, a fade). Never for game logic or I/O.
- No third-party async library (UniTask etc.).

## 9. Errors, logging, comments
- Expected failures (invalid experiment, refused request, network error) are **values**: return `Result<T>`-style objects with a list of `Diagnostic { Code, Message, Path }`. No exceptions for control flow.
- Exceptions only for programmer errors (`ArgumentNullException` on public Core entry points, impossible states).
- `Core` does not log. Unity layers log with `Debug.Log/LogWarning/LogError` and a short prefix `[Authoring]`, `[Quest]`, `[Net]`, `[Lab]`. Pass the context object as the second argument when one exists. No log spam in `Update`.
- User-visible errors are shown in the UI, not only in the console.
- Comments explain **why**, never what. No commented-out code. TODOs carry the story ID: `// TODO(S2.1): ...`.

## 10. GC and performance (Quest target)
- No allocations in `Update`, `FixedUpdate`, or per-frame simulation `Advance` paths: no `new` of reference types, no LINQ, no string concatenation, no boxing. Reuse lists (`Clear()`).
- No `GetComponent`, `Find*`, `Camera.main` per frame; cache in `Awake`/`Init`.
- Particle counts and lights are budgeted per scene (measured in SP-5). Quest scenes: mobile URP settings, no real-time shadows unless measured.
- Core simulation steps at a fixed rate chosen in its tech-spec; presentation interpolates.

## 11. Security and data
- Never commit secrets (ADR-006). Config keys are read from environment or gitignored local files.
- Treat every downloaded or AI-produced JSON as untrusted: validate with `Core` before use.
- Never use `TypeNameHandling` in Newtonsoft.

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
namespace LabKit.Core.Validation
{
    /// <summary>Checks an experiment against the catalog and returns all problems found.</summary>
    public sealed class ExperimentValidator
    {
        private readonly Catalog _catalog;

        public ExperimentValidator(Catalog catalog)
        {
            _catalog = catalog ?? throw new ArgumentNullException(nameof(catalog));
        }

        public ValidationResult Validate(Experiment experiment)
        {
            var result = new ValidationResult();
            foreach (var container in experiment.Setup.Containers)
            {
                if (!_catalog.HasContainerKind(container.Kind))
                {
                    result.Add("unknown-container-kind", $"Unknown kind '{container.Kind}'.", $"setup.containers[{container.Id}]");
                }
            }
            return result;
        }
    }
}
```

Thin MonoBehaviour adapter:
```csharp
namespace LabKit.Lab
{
    public sealed class ContainerView : MonoBehaviour
    {
        [SerializeField] private Renderer _liquidRenderer;

        private Simulation _simulation;
        private string _containerId;

        public void Init(Simulation simulation, string containerId)
        {
            _simulation = simulation;
            _containerId = containerId;
        }

        private void Awake()
        {
            if (_liquidRenderer == null)
            {
                Debug.LogError($"[Lab] {name}: _liquidRenderer is not assigned.", this);
                enabled = false;
            }
        }

        private void OnEnable()  { if (_simulation != null) _simulation.EventRaised += OnSimEvent; }
        private void OnDisable() { if (_simulation != null) _simulation.EventRaised -= OnSimEvent; }

        private void OnSimEvent(SimEvent e) { /* update visuals only; no game logic */ }
    }
}
```

Test:
```csharp
[Test]
public void Validate_UnknownContainerKind_ReturnsDiagnostic()
{
    var validator = new ExperimentValidator(TestCatalogs.Minimal());
    var result = validator.Validate(TestExperiments.WithContainerKind("nope"));
    Assert.That(result.Has("unknown-container-kind"), Is.True);
}
```
Note: `Init` is called before `OnEnable` only if the object is created inactive or the bootstrap calls it before enabling; the tech-spec of a view must state the order.

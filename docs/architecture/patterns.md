# Approved Patterns

Status: Active, rewritten 2026-10-15 for Solo Tutor (previous version: git history, commit `4e151cf`). Use only these. Anything else needs an ADR first (see `dev-workflow.md` section 7). Every pattern traces to a need in the architecture (ADR numbers) and, when PM IDs exist, to a story.

## Approved

### 1. Plain C# domain + thin MonoBehaviour adapter
- **Use when:** any logic that needs tests or may run outside a scene (all of `Core`).
- **Don't:** put branching logic in a MonoBehaviour.
- **Example:** `ExerciseSession` (plain) is observed by `ExerciseScreen` (MonoBehaviour). See `coding-standards.md` section 13.

### 2. Action as data
- **Use when:** something the student does must be checked, recorded or sent as JSON: an answer, a `StudentAction` on the 3D bench (pipette volume, fill to mark), an `Attempt` (ADR-002, 013).
- **Don't:** add undo/redo or command queues.
```csharp
public abstract record StudentAction;
public sealed record PipetteAction(string FromId, string ToId, double VolumeMl) : StudentAction;
// session.Apply(new PipetteAction("stock", "flask", 25));
```
(If the C# version in use lacks records, use sealed classes with readonly properties. Records need an `IsExternalInit` shim on `netstandard2.1`: decide in SP-3.)

### 3. Exercise family (strategy)
- **Use when:** one type of exercise has its own generation, answer and wrong-rule logic. Cap: 4 families in the first release (ADR-002).
```csharp
public interface IExerciseFamily
{
    string Id { get; }
    ExerciseInstance Build(ExerciseSpec spec);
    CheckResult Check(ExerciseInstance instance, Answer answer);
}
```
- **Don't:** one class per exercise variant; add data (ranges, tags) instead.

### 4. Data-driven content
- **Use when:** skills, brick ranges, difficulty bands, error-tag labels, facts. JSON in `Data/Content/` (ADR-011). ScriptableObjects only for presentation mapping.
- **Don't:** hard-code a fact, range or label in C#.

### 5. C# events from logic to presentation
- **Use when:** a plain class notifies views (`event Action<...>`).
- **Don't:** use `UnityEvent` for code wiring, SendMessage, global buses, or ScriptableObject event channels.

### 6. Provider/adapter with a mock
- **Use when:** two real implementations exist: `IExerciseComposer` (`SeededComposer`, `AiComposer`), `IApiClient` (real `UnityWebRequest` client, fake for tests and offline), the AI transport (real, recorded) (ADR-003, 005).
- **Don't:** create an interface for a class with one implementation and no test seam.

### 7. Composition root with constructor injection
- **Use when:** wiring objects in a Unity scene: one `*Bootstrap` MonoBehaviour per scene (ADR-010). On the server, the built-in ASP.NET Core container in `Program.cs`.
- **Don't:** singletons, `FindObjectOfType`, service locator, third-party DI container in Unity.

### 8. Result with diagnostics
- **Use when:** validation, checking and network calls that can fail in expected ways.
```csharp
public sealed class ValidationResult
{
    private readonly List<Diagnostic> _items = new();
    public bool IsValid => _items.Count == 0;
    public IReadOnlyList<Diagnostic> Items => _items;
    public void Add(string code, string message, string path) { _items.Add(new Diagnostic(code, message, path)); }
}
```
- **Don't:** throw for invalid input.

### 9. Derive, don't store (pure policy functions)
- **Use when:** mastery, XP, level, streak, next skill, quota decisions can be recomputed from the attempt list and a clock value: `MasteryCalculator`, `Progression`, `TutorPolicy`, `QuotaPolicy` are pure functions in `Core` (ADR-003, 007). The server may cache the result as a profile summary.
- **Don't:** keep a second source of truth that can drift from the attempts; read the system clock inside a policy.

### 10. Validate-and-repair around the AI
- **Use when:** any AI output reaches a student: parse -> validate (Core) -> on failure send diagnostics back (max 2 repairs) -> fallback to code (ADR-003).
- **Don't:** show unvalidated AI output, or retry without a cap.

### 11. Screen controller + session model (UI)
- **Use when:** each screen (login, exercise, feedback, profile) is a view with one controller MonoBehaviour reading and updating a plain session object (current exercise, hints used, last result, step enum). Web and Quest shells each have their own views over the same `Core` session.
- **Don't:** a full MVP/MVVM framework, a navigation framework, data-binding libraries.

### 12. Enum-based flow state
- **Use when:** a flow has a handful of steps (`SignedOut`, `Loading`, `Answering`, `Reviewing`).
- **Don't:** a state-machine library or state classes unless a step gets real sub-logic.

### 13. Thin endpoints, services, repositories (server only)
- **Use when:** a minimal API endpoint parses and authorizes, a service holds the use case, EF Core `DbContext` is used inside services (no repository layer on top of EF Core).
- **Don't:** controllers/MediatR/CQRS frameworks, generic repositories.

## Not approved (now)

| Pattern | Reason |
|---|---|
| DI container in Unity (VContainer, Zenject) | No story needs scopes; revisit per ADR-010 |
| Service locator, singletons | Hidden dependencies |
| ScriptableObject event channels | C# events suffice |
| Object pooling | No entity count demands it; add only after a measured problem |
| State machine library | Enum is enough |
| MVP/MVVM frameworks, UI data binding | Overkill for a handful of screens |
| ECS/DOTS | No scale need |
| UniTask/UniRx | Plain async + events are enough (and WebGL rules, ADR-008) |
| Community ratings, teacher dashboard | ADR-014 (deferred) |
| Embeddings / vector memory, storing chat | ADR-003, 006 |
| MediatR, CQRS, microservices, message queues | Server is small; ADR-005 |
| Offline attempt queue | Deferred; attempt API is idempotent so it can be added later |

# Approved Patterns

Status: Active, 2026-10-14. Use only these. Anything else needs an ADR first (see `dev-workflow.md` section 7). Every pattern traces to a need in the architecture (ADR numbers) and, when PM IDs exist, to a story.

## Approved

### 1. Plain C# domain + thin MonoBehaviour adapter
- **Use when:** any logic that needs tests or may run outside a scene (all of `Core`).
- **Don't:** put branching logic in a MonoBehaviour.
- **Example:** `Simulation` (plain) is observed by `ContainerView` (MonoBehaviour). See `coding-standards.md` section 13.

### 2. Action as data (command)
- **Use when:** something the player or a script does must be recorded, replayed, validated or sent as JSON: the reference solution, mistake probes, keyboard and XR input (ADR-002, ADR-010).
- **Don't:** add undo/redo or command queues; not needed.
```csharp
public abstract record LabAction;
public sealed record PourAction(string From, string To, double AmountMl) : LabAction;
// simulation.Apply(new PourAction("acid-bottle", "beaker-1", 10));
```
(If the C# version in use lacks records, use sealed classes with readonly properties.)

### 3. Rule family (strategy)
- **Use when:** a generic mechanism is driven by data tables (`MixingHeat`, `Neutralization`, `Threshold`). Cap: 2-3 families in the first release (ADR-002).
```csharp
public interface IRuleFamily
{
    void Evaluate(WorldState state, IEventSink events);
}
```
- **Don't:** one class per reaction; add data rows instead.

### 4. Data-driven catalog
- **Use when:** substances, containers, rule parameters, rule-card text. JSON in `Data/Catalog/` (ADR-008). ScriptableObjects only for presentation mapping.
- **Don't:** hard-code a substance, number or card text in C#.

### 5. C# events from simulation to presentation
- **Use when:** `Simulation` notifies views (`event Action<SimEvent>`).
- **Don't:** use `UnityEvent` for code wiring, SendMessage, global buses, or ScriptableObject event channels (not needed at this size).

### 6. Provider/adapter with a mock
- **Use when:** two real implementations exist: `IExperimentAuthor` (`MockAuthor`, `ServerAuthor`), `IExperimentSource` (local file, HTTP by code) (ADR-005).
- **Don't:** create an interface for a class with one implementation and no test seam.

### 7. Composition root with constructor injection
- **Use when:** wiring objects in a scene: one `*Bootstrap` MonoBehaviour per scene (ADR-007).
- **Don't:** singletons, `FindObjectOfType`, service locator, DI container.

### 8. Result with diagnostics
- **Use when:** validation, verification and network calls that can fail in expected ways.
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

### 9. Screen controller + session model (authoring UI)
- **Use when:** each authoring screen (Chat, Summary, Review, Preview, Publish) is a UI Toolkit view (UXML/USS) with one controller MonoBehaviour that reads and updates a plain `AuthoringSession` object (current experiment, verification report, step enum).
- **Don't:** a full MVP/MVVM framework; navigation framework; data-binding libraries.

### 10. Enum-based flow state
- **Use when:** the authoring flow has a handful of steps (`Chatting`, `Reviewing`, `Previewing`, `Publishing`).
- **Don't:** a state-machine library or state classes unless a step gets real sub-logic.

## Not approved (now)

| Pattern | Reason |
|---|---|
| DI container (VContainer, Zenject) | No story needs scopes; revisit per ADR-007 |
| Service locator, singletons | Hidden dependencies |
| ScriptableObject event channels | C# events suffice |
| Object pooling | No entity count demands it; add only after a measured problem |
| State machine library | Enum is enough |
| MVP/MVVM frameworks, UI data binding | Overkill for 5 screens |
| ECS/DOTS | No scale need |
| UniTask/UniRx | Plain async + events are enough |
| Community ratings, accounts | ADR-011 |
| Embeddings / vector memory | ADR-005 |

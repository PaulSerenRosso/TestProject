# ADR-007: Plain constructor injection, no DI container

Status: Accepted (2026-10-14)

## Context
Dependency injection (DI) = passing a class what it needs instead of letting it fetch it. Needed for tests and for swapping mock/real implementations.

## Options
| Option | Verdict |
|---|---|
| Singletons / service locator / `FindObjectOfType` | Rejected: hidden dependencies, hard to test. |
| DI framework (VContainer, Zenject) | Rejected for now: setup and learning cost; no story needs scopes or lifetimes. Versions not verified. Revisit only if the composition code exceeds about 100 lines per scene. |
| **Constructor injection by hand + one composition root per scene** | **Chosen** |

## Decision
- Core and Net classes receive dependencies through constructors; no static mutable state.
- One `*Bootstrap` MonoBehaviour per scene (the composition root) creates objects and wires them (for example `new ExperimentVerifier(rules, simulationFactory)`).
- MonoBehaviours get dependencies through an `Init(...)` method called by the bootstrap, never by `Find` or singletons.
- Interfaces only where there are two real implementations or a test seam (see `patterns.md`).

## Consequences
- Easy to explain in an interview: pattern yes, framework deliberately not yet.
- Wiring is explicit and readable in one place per scene.

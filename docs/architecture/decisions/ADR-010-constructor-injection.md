# ADR-010: Plain constructor injection, no DI container

Status: Accepted (2026-10-15). Carried over from Lab Kit ADR-007.

## Context
Dependency injection (DI) = passing a class what it needs instead of letting it fetch it. Needed for tests and for swapping mock and real implementations (composer, API client).

## Options
| Option | Verdict |
|---|---|
| Singletons / service locator / `FindObjectOfType` | Rejected: hidden dependencies, hard to test. |
| DI framework in Unity (VContainer, Zenject) | Rejected for now: setup and learning cost; no story needs scopes or lifetimes. Revisit if the composition code exceeds about 100 lines per scene. |
| **Constructor injection by hand + one composition root per scene** | **Chosen** |

## Decision
- `Core` and `Net` classes receive dependencies through constructors; no static mutable state.
- One `*Bootstrap` MonoBehaviour per scene (the composition root) creates and wires objects.
- MonoBehaviours get dependencies through an `Init(...)` method called by the bootstrap, never by `Find` or singletons.
- On the server, ASP.NET Core's **built-in** DI is used as intended (it ships with the framework); `Core` classes stay container-agnostic and are registered in `Program.cs`.
- Interfaces only where there are two real implementations or a test seam (`patterns.md`).

## Consequences
- Easy to explain in an interview: pattern yes, third-party Unity framework deliberately not yet.
- Wiring is explicit and readable in one place per scene.

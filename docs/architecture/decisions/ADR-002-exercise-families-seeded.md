# ADR-002: Exercise families with seeded generation and code-computed answers

Status: Accepted (2026-10-15). Replaces Lab Kit ADR-002 (quantity simulation with rule families).

## Context
Exercises are parametrized tasks (dilution, balancing, mole, particle zoom), not free experiments. Correctness must be guaranteed by code. The same exercise must be reproducible on web, Quest and server, and typical student mistakes must be recognized and labeled.

## Options
| Option | Verdict |
|---|---|
| Continuous quantity simulation with hazard rules (Lab Kit) | Rejected: the product no longer needs emergent consequences; big cost for no story. |
| Hard-coded exercise lists | Rejected: no variety, no adaptive difficulty. |
| **Exercise families: code per type, data for ranges, seeded generation** | **Chosen** |
| Let the AI also write the solution or check code | Rejected: the AI would own correctness (see ADR-003). |

## Decision
- An `ExerciseFamily` is a C# class in `Tutor.Core` per exercise type. It turns an `ExerciseSpec` into an `ExerciseInstance`, computes the correct answer, and checks a student answer with **wrong-rule recomputation** returning an `ErrorTag` (for example `unit-ml-l`, `swapped-ratio`).
- Parameter ranges, difficulty bands, tag labels and fact ids live in `bricks.json` (ADR-011), not in code.
- `SeededComposer` produces specs from a seed with an own PRNG (`Pcg32`), never `System.Random` or the clock, so the same seed gives the same spec on every platform. Golden-seed fixtures detect drift (ADR-012).
- Hard cap for the first release: **4 families** (dilution, balancing + limiting reagent, mole by weighing, particle zoom diagnostic). A new family needs a backlog story and a teacher-reviewed rule table.
- Spatial interaction (dilution bench in 3D) emits `StudentAction`s (data) that the family checks, so web and VR share the checker.

## Consequences
- New exercise variants cost no code; a new type costs one class + data + tests.
- The cost moves to correct content and review (Q2), not engine code.
- `Core` stays free of Unity, threads, time, I/O (it also runs on the server).

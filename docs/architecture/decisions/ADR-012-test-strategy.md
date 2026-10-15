# ADR-012: Test strategy

Status: Accepted (2026-10-15). Adapted from Lab Kit ADR-009. Shared-test feasibility is checked in SP-3.

## Context
Most logic is pure C# in `Core`, which also compiles on the server. Owner wants real unit tests (cheap with AI-assisted development).

## Decision
| Kind | What | Where / how |
|---|---|---|
| Unit (NUnit) | Families, checkers, wrong-rule tags, validator, `AnswerGuard`, mastery, progression, policy, quota, PRNG, JSON round-trips | `Tests/EditMode/Core/`, run in Unity Test Runner **and** by `dotnet test` (project `server/Tutor.Core.Tests` links the same files) |
| Property tests | Over many seeds per family (ADR-004) | same |
| Golden seeds | Fixed seed + difficulty -> expected spec; catches PRNG or generator drift across platforms | `Tests/Fixtures/Exercises/` |
| Worked examples | Programme/textbook examples with source reproduced by the family | same |
| AI client | Recorded real responses replayed by a fake transport; invalid and adversarial samples included. **No live API calls in tests.** | Core tests + server tests |
| Server | API tests with `WebApplicationFactory` and an in-memory/temporary SQLite: auth, quota atomicity, attempt idempotency, delete/export, no chat column | `server/Tutor.Server.Tests` |
| PlayMode smoke | Web scene loads and logs in against a fake; Quest scene wiring | Few tests only |
| Manual | VR feel, visuals, WebGL in real browsers, performance on device | Checklist in each tech-spec |

- Test naming `Method_Condition_Expected`. Deterministic: no sleeping, no network, no real clock (inject a clock into the server).
- Gate before every commit: `dotnet test` (fast, no Unity needed) plus the Unity EditMode run when Unity code changed (Unity CLI `run_tests`, or batch mode `-runTests`; exact flags confirmed against Unity docs in the dev-workflow task). Local pre-push script runs them.
- CI (GitHub Actions) becomes realistic for `dotnet test` because it needs no Unity license. Unity CI (GameCI) stays deferred: Personal-license activation reported broken/changed (https://discussions.unity.com/t/unity-no-longer-supports-manual-activation-of-personal-licenses/926760, accessed 2026-10-14, UNVERIFIED).
- Proportion: test logic and data contracts; do not unit-test MonoBehaviour plumbing.

## Consequences
- Rule or validator bugs are caught in seconds without Unity or a headset.
- Core tests must avoid Unity APIs (including `UnityEngine.Assertions`) and locate fixtures through a shared path helper.

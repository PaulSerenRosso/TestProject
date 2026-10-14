# ADR-009: Test strategy

Status: Accepted (2026-10-14)

## Context
Owner wants real unit tests (cheap with AI-assisted development). Core is pure C#, so most logic is testable without Unity scenes.

## Decision
| Kind | What | Where / how |
|---|---|---|
| Unit (EditMode, NUnit) | Rule families, simulation, objective checks, validator, JSON round-trips, verifier, rule-card lookup, mock author | `LabKit.Core.Tests` |
| Golden experiments | Every file in `Tests/Fixtures/Experiments/` must validate; its reference solution must reach the objective; each probe must fire its event | Parameterized test over the folder |
| Cross-validation | Our model vs reference fixtures within tolerance (ADR-003) | `Tests/Fixtures/CrossVal/` |
| AI client | Recorded real responses replayed by a fake transport. **No live API calls in tests.** | `LabKit.Core.Tests` / Net tests |
| PlayMode smoke | Scene loads, bootstrap wires, one scripted pour runs | Few tests only |
| Manual | XR feel, visuals, performance on device | Checklist in each tech-spec |

- Test naming `Method_Condition_Expected`. Tests are deterministic; no sleeping, no network, no real clock.
- Run before every commit: EditMode suite through the Unity CLI `run_tests`, or batch mode (`-runTests`; exact flags to be confirmed against Unity docs in the dev-workflow task). Hook: a local pre-push script runs the suite.
- CI (GitHub Actions + GameCI) deferred: license activation for Personal licenses reported broken/changed by a forum thread (https://discussions.unity.com/t/unity-no-longer-supports-manual-activation-of-personal-licenses/926760, accessed 2026-10-14, UNVERIFIED). Local gate first.
- Proportion: test logic and data contracts; do not unit-test MonoBehaviour plumbing.

## Consequences
- Bugs in rules or validation are caught without a headset.
- Every new rule family ships with unit tests and, where a reference exists, a fixture.

# ADR-002: Rule-driven simulation ("level B")

Status: Accepted (2026-10-14)

## Context
The pitch is "the mistake is the lesson". Mistakes must emerge from what the student does, not from a script of known wrong paths. The AI must generate many experiments without new code per experiment. The owner fears building a chemistry engine.

## Options
| Option | Verdict |
|---|---|
| A. Scripted step graph with authored "wrong step" branches | Rejected: only the mistakes the AI thought of exist; AI invents behavior; hallucination-prone. |
| **B. Rule-driven simulation**: AI composes initial state + objective; authored rules react to any action | **Chosen** |
| C. Real chemistry engine (first principles) | Rejected: huge scope; native libraries on Quest; engines give equilibrium states, not hazard events (splash, boil-over). |

## Decision
- Simulation is plain C# in `LabKit.Core`: deterministic, no UnityEngine, no randomness, no wall-clock. `Apply(LabAction)` and `Advance(dt)` emit `SimEvent`s.
- State is quantity-based: containers hold (substanceId, amountMl), temperatureC. No fluid simulation; the pour stream is a particle effect driven by the pour rate.
- Behavior comes from a few **rule families** driven by data tables (candidates: mixing heat, neutralization, threshold events). **Hard cap for the first release: 2 or 3 families**, chosen by the first experiment. Each new family needs a backlog story.
- Rules and their data are authored by the owner, each with a `source`. The AI only selects catalog IDs.
- Unknown combinations: "no notable effect" in the sandbox; the AI is told the catalog and must refuse or propose alternatives outside it.

## Consequences
- New experiment = no new code if the bricks exist. A missing brick triggers the refusal path.
- Cost moves to data curation (correct numbers), not engine code. The AI can help draft tables; a human must verify them.
- The same code serves tests, headless verification (ADR-004) and gameplay.
- Realism is limited to the covered cases; rule cards state the supported range.

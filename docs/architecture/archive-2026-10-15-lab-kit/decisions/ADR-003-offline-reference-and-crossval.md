# ADR-003: Scientific engines offline; cross-validation by committed fixtures

Status: Accepted (2026-10-14). Feasibility for the first experiment UNVERIFIED (SP-4).

## Context
The owner is not a chemist and a teacher cannot audit the calculations. Existing tools (Cantera, PHREEQC/IPhreeqc, RDKit) are native or Python libraries: no maintained C#/Unity path found (searches 2026-10-14; Cantera .NET API is experimental; PHREEQC offers COM/DLL only).

## Options
| Option | Verdict |
|---|---|
| Embed a chemistry engine in the player | Rejected: Android ARM64 native builds, wrappers, unproven; still needs hazard-event rules. |
| Trust hand-written formulas | Rejected: not defensible. |
| **Use a reference tool offline; compare our model against its output in tests** | **Chosen** |

## Decision
- `tools/crossval/<family>.py` runs the reference tool (PHREEQC via Python, or a lookup of a published table) on listed cases and **writes** `Assets/_Project/Tests/Fixtures/CrossVal/<family>.json`: tool name, version, date, tolerance, cases (inputs, expected). The owner runs it manually when a family or rule changes; the fixture and the script are committed.
- A C# EditMode test loads the fixture, runs `Core` on the same inputs and asserts results within tolerance. **Tests never run Python** (no Python needed to clone and test; deterministic).
- The rule card badge reads fixture metadata: "Validated against PHREEQC 3.x, tolerance 0.1 pH, 2026-10-20". A rule without a fixture shows `Not cross-validated`.
- If no engine fits (for example concentrated acid), use a published table as reference and name it in the metadata.

## Consequences
- The test proves agreement only for the listed cases; the card shows tool, tolerance and supported range.
- Python is needed only by the owner for regeneration.

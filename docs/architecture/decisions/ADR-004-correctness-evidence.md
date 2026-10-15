# ADR-004: Correctness evidence without a reference engine

Status: Accepted (2026-10-15). Replaces Lab Kit ADR-003 (PHREEQC cross-validation).

## Context
The owner is not a chemist. Seconde exercises are arithmetic and counting (dilution, mole, balancing, limiting reagent, Lewis octets). A scientific engine adds nothing here, but wrong content would destroy trust.

## Options
| Option | Verdict |
|---|---|
| Reference engine offline (PHREEQC, Cantera) | Rejected: no seconde brick needs it. |
| Trust hand-written formulas | Rejected: not defensible. |
| **Layered evidence: property tests + independent second implementation where cheap + worked examples with sources + teacher review status** | **Chosen** |

## Decision
- **Property tests** per family over many seeds: the correct answer passes the checker; every wrong-rule answer yields its tag and is not accepted; values stay in realistic ranges.
- **Independent check** where cheap: balanced equations verified by atom counting; a brute-force solver compared with the closed-form one for limiting reagent.
- **Worked examples** from the 2019 programme annex or textbooks live in `Tests/Fixtures/Exercises/` with their source; the family must reproduce them.
- **Reference data** (periodic table to Z = 18, listed ions) comes from a cited table committed as content.
- **Review status** on every brick and fact: `Reviewed by <role>, <date>` or `Unreviewed`, shown in the UI (ADR-014). Target: one seconde teacher reviews rule tables (Q2).
- Python and `tools/crossval` are not created.

## Consequences
- Honest and cheap; proof is "tests + sources + reviewer", not "validated by an engine".
- If a later brick needs a real engine (titration curves are première+), reopen with a new ADR.

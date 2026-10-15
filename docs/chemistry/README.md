# Chemistry expert memory

Last update: 2026-10-15 (reorganized into projects/). Kept by the `chemistry-education-expert` agent.

## 1. Project and target
- The owner (French, not a chemist) builds a Unity portfolio. Two chemistry projects live here, kept apart:
  - **solo-tutor (current, 2026-10-15)**: AI tutor + VR/PC solo practice for **seconde**. Start at `projects/solo-tutor/concept.md`.
  - **lab-kit (earlier)**: AI-assisted teacher lab kit (desktop authoring app + Quest VR runtime), collège. See `projects/lab-kit/`, `docs/brainstorms/vr-teacher-lab-kit.md` and `docs/architecture/architecture-overview.md`.
- Layout: `notes/` = shared chemistry knowledge; `projects/<name>/` = notes specific to one project.

## 2. Notes
**Shared (`notes/`)**
| Note | Summary | Date |
|---|---|---|
| [learning-and-practice-overview](notes/learning-and-practice-overview.md) | How chemistry is learned and practiced; virtual lab and simulation use; evidence | 2026-10-15 |
| [college-student-struggles](notes/college-student-struggles.md) | Collège struggles (macro-micro link, dissolving, mass conservation) | 2026-10-15 |

**solo-tutor (current)**
| Note | Summary | Date |
|---|---|---|
| [concept](projects/solo-tutor/concept.md) | Clarified concept, owner decisions, open decisions, bricks, demo slice | 2026-10-15 |
| [initial-assessment-college](projects/solo-tutor/initial-assessment-college.md) | First honest assessment (written for collège): risks, ranked exercises, MVP | 2026-10-15 |
| [target-level-analysis](projects/solo-tutor/target-level-analysis.md) | Collège vs seconde deep dive, programme content, exercise ideas, recommendation | 2026-10-15 |

**lab-kit (earlier project)**
| Note | Summary | Date |
|---|---|---|
| [app-usefulness-vr-lab](projects/lab-kit/app-usefulness-vr-lab.md) | Verdict on the teacher lab kit idea, challenges, best chemistry area for a PoC | 2026-10-15 |

## 3. Decisions and findings so far
- Virtual and hands-on labs give similar conceptual scores; hands-on is better for physical technique (RSC 2013).
- VR chemistry barriers: cost, teacher training, few long-term studies; Quest 2 chemistry apps felt awkward to students (Maribor 2024).
- Real value of the idea is narrower than the brainstorm: pre-lab safety and procedure rehearsal, with teacher-parametrized variants (judgment).
- Best chemistry area for a small proof of concept: inorganic/general bench chemistry (dilution, acid-base), or titration (judgment). Organic is too complex.
- Owner goal: pre-lab rehearsal, not lab replacement. VR is the weakest part for pre-lab (students lack headsets at home); PC/browser should be the main path, VR optional (judgment).
- Premade vetted templates + AI filling constrained slots beats free generation; per-student numbers are better done by a form (judgment).
- For collège, the best-documented struggles are the macro-micro link, particles given material properties, dissolving and mass conservation. The invisible particle level is the strongest value; danger/cost is secondary (judgment). Earlier dilution/titration findings target lycée/university.
- Teacher review builds trust on intent; precision must come from sourced rules and honest review status (judgment).
- New concept (2026-10-15): solo AI-tutor practice for collège. Code owns correctness, AI only picks bricks/explains from a fact sheet; home = PC only, VR school-only bonus; student memory kept local/pseudonymous (CNIL: under 15 needs parent consent); MVP = dissolving and mass conservation, 3 brick types, desktop first (judgment).
- Level deep dive (2026-10-15; owner then chose seconde): with VR, gamification and AI weighted equally, seconde scores slightly higher than collège (AI tutor and consent favor seconde, gamification favors collège). Seconde = calculations (g/L dilution, mole, balancing, limiting reagent), mostly code-verifiable; molar mass and mol/L are first-year only. Suggested: seconde core + a 3e prerequisite diagnostic as a bridge layer; VR hero brick = dilution bench. Read in full: Éduscol cycle 4 (2016) and seconde annex (2019); première spé was a draft, terminale not read.
- Official hooks: seconde text asks for automatismes and work outside class; cycle 4 Éduscol resource recommends diagnostics and microscopic simulations. Cycle 4 order is the teacher's choice, so map bricks to skills, not school years.
- Nuance: in the Éduscol example, pH starts in 5e and chemical mass conservation is 3e (earlier notes said pH 3e, mass 5e).
- AI rules (press relay, official page not reachable): national AI framework 14 June 2025 allows supervised classroom generative AI from 4e; AI Pix training compulsory in 4e and 2de. Consent under 15 needs child plus parent (CNIL).
- Safety fact to keep: add acid slowly to water, never the reverse.

## 4. Open questions
- Can the owner reach one collège physique-chimie teacher for a 20-minute check?
- Priority: invisible particle level vs a spectacular experiment; teacher usefulness vs portfolio showcase?
- Compare 2-3 candidate collège experiments against the programme (what VR adds over an animation).
- Meta age rules (11-15) and GDPR for minors with an AI server (unverified).
- VR vs desktop virtual lab studies not yet verified by search.
- Official French programme texts: seconde read; cycle 4 only via Éduscol 2016 resource; première spé draft; terminale not read.
- Owner decisions (2026-10-15): target = seconde; VR and PC equal; cloud pseudonymous profile; no chat logs stored; test values only. Still open: audience (portfolio vs also teachers), teacher review of bricks, AI provider and cloud host.
- Not found: national VR headset counts per level, at-home practice market size, seconde misconception papers (full text), school-managed Quest rules.
- Usage of Labster / ChemCollective not verified by search.

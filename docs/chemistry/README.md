# Chemistry expert memory

Last update: 2026-10-15. Kept by the `chemistry-education-expert` agent.

## 1. Project and target
- The owner (French, not a chemist) builds a portfolio project: an AI-assisted teacher lab kit (desktop authoring app + Quest VR runtime). See `docs/brainstorms/vr-teacher-lab-kit.md` and `docs/architecture/architecture-overview.md`.
- Target teacher: not fixed. The owner leans international; France (lycee, early university) is the owner's own context. Curriculum choice is still open.

## 2. Notes
| Note | Summary | Date |
|---|---|---|
| [learning-and-practice-overview](notes/learning-and-practice-overview.md) | How chemistry is learned and practiced (high school, university, professional); virtual lab and simulation use; evidence | 2026-10-15 |
| [app-usefulness-vr-lab](notes/app-usefulness-vr-lab.md) | Honest verdict on the app idea, challenges, and which chemistry area fits a small proof of concept | 2026-10-15 |

## 3. Decisions and findings so far
- Virtual and hands-on labs give similar conceptual scores; hands-on is better for physical technique (RSC 2013).
- VR chemistry barriers: cost, teacher training, few long-term studies; Quest 2 chemistry apps felt awkward to students (Maribor 2024).
- Real value of the idea is narrower than the brainstorm: pre-lab safety and procedure rehearsal, with teacher-parametrized variants (judgment).
- Best chemistry area for a small proof of concept: inorganic/general bench chemistry (dilution, acid-base), or titration (judgment). Organic is too complex.
- Owner goal: pre-lab rehearsal, not lab replacement. VR is the weakest part for pre-lab (students lack headsets at home); PC/browser should be the main path, VR optional (judgment).
- Premade vetted templates + AI filling constrained slots beats free generation; per-student numbers are better done by a form (judgment).
- Safety fact to keep: add acid slowly to water, never the reverse.

## 4. Open questions
- Which curriculum and education level to target (France lycee, university, international)?
- Is the owner willing to pitch the app as "pre-lab rehearsal with AI-generated variants" rather than a lab replacement?
- Can the owner reach one real teacher or lab technician for a 20-minute check?
- Where do students do the pre-lab, and is the portfolio showcase or teacher usefulness the priority?
- VR vs desktop virtual lab studies not yet verified by search.
- Official French programme texts (Bulletin officiel) not yet verified.
- Usage of Labster / ChemCollective not verified by search.

# Concept: AI chemistry tutor, solo practice in VR or on PC (seconde)

Date: 2026-10-15
Status: concept clarified with the owner. Input for brainstorm, project-manager and tech-architect. Not a scoped project yet.
Supporting analysis: `initial-assessment-college.md` (risks, ranked exercises) and `target-level-analysis.md` (level comparison, programme content, sources).
Do not confuse with the earlier project `../lab-kit/` (teacher authoring app + VR runtime).

## 1. One-line pitch
A solo chemistry practice app for French lycée students (seconde): the same exercises in VR (school headsets) or on PC (home), gamified, with an AI tutor that picks the next exercise, adapts difficulty, explains and remembers the student across devices. It helps when the teacher is not there; it does not replace the teacher.

## 2. Decisions (made by the owner)
| Topic | Decision |
|---|---|
| Target level | **Seconde** (lycée). 3e skills appear only as a prerequisite diagnostic, not as a second audience |
| Platforms | **VR and PC, equal weight**, both in the demo |
| Pillars | VR, gamification and AI tutoring weighted **equally** |
| Student memory | **Cloud**, so a student can start in VR at school and continue on PC at home |
| Privacy approach | Pseudonymous profile; **do not store the chat discussions** |
| Data in the portfolio | **Test values only**, never real children |
| Role of AI | Custom tutor outside class hours; not a teacher replacement |
| Correctness | Exercise bricks are programmed, factual and code-checked |

## 3. Decisions NOT yet made
- Real audience of the demo: portfolio viewers only, or also seconde teachers (changes classroom fit vs wow).
- Whether a real seconde teacher will review the bricks (strongly recommended; see risks).
- AI provider and cloud host (EU region, no training on data, processing agreement if ever used for real).
- Backend choice and account/login method (class code, parent-created login, test accounts).

## 4. How it works
1. **Bricks (code).** A brick is a parametrized exercise template: parameter ranges, a code-computed correct answer, typical wrong-rule recomputation (to label the error, for example "forgot mL to L"), a short sourced explanation, a misconception/error tag, and a difficulty level. Same brick, same seed and same checker on VR and PC.
2. **Student profile (cloud, pseudonymous).** Per student: pseudonymous id, brick id, seed, answer, error tag, mastery per skill. No name. No chat logs.
3. **AI tutor.** Picks the next brick from the profile and a skill graph, adjusts difficulty, rewrites hints at the student's level, answers questions only from a fixed fact sheet built from the bricks, and says "ask your teacher" outside it. It never judges an answer; code does. Refuses dangerous "how do I make..." questions.
4. **Diagnostic bridge.** A short 3e-prerequisite check (particles, atom counts, formulas, density, solubility, pH) places the student on the skill graph: particles, atoms, formulas, mole, balancing, limiting reagent, dilution.
5. **Teacher summary (optional, later).** Weekly view of which error tags were hit.

## 5. Seconde content to build on (from the 2019 programme annex)
Mass concentration (g/L), dilution and glassware choice, the mole and counting entities, writing and balancing equations, limiting reagent, Lewis diagrams and electron configurations (to 3p). Not in seconde: molar mass and mol/L (première).

## 6. Candidate demo slice (about 4 brick families)
| Brick | PC | VR | Code-checkable |
|---|---|---|---|
| Dilution bench (client order: make 100 mL at X g/L; choose glassware, compute volume, pipette, fill to mark) | yes | **hero brick**: hand and eye rehearsal | yes |
| Reactor chef (balance an equation, then find what runs out) | yes | build molecules, watch consumption | yes |
| Mole as counting by weighing (grams to number of entities) | yes | low value (scale zoom only) | yes |
| Particle zoom (diagnostic/bridge, collège level) | yes | stand inside the flask | yes (rule table) |

Rule for every brick: ask "what does VR add over PC?" If nothing, ship it PC-only and say so.
More ideas (Lewis and ion builder, mystery concentration, identify the unknown): see `target-level-analysis.md` section 3.

## 7. Principles
- Code owns correctness; AI orchestrates and explains.
- Gamification layered on real tasks (client orders, production line, case files), not a quiz in disguise.
- Safety: hazardous reactions stay virtual, no imitable quantities or steps; add acid to water, never the reverse.
- Honest pitch: VR adds presence and motivation; there is no proof it teaches better than PC at this age.

## 8. Risks (short)
- Seconde can feel like a worksheet; gamification is the weakest pillar at this level.
- A non-chemist must have every brick and rule table reviewed by a teacher.
- Equal weight on three pillars plus two platforms is a solo-dev scope risk.
- Seconde is mostly 15 or older (consent easier), but real use would still need GDPR work and, for AI steering learning, EU AI Act checks. Irrelevant for a test-data demo, relevant before real use. Not legal advice.
- Evidence gaps: at-home market, competing platforms, VR learning benefit, seconde misconception studies.

## 9. GDPR cheat sheet (for later, if real users)
Consent: from 15 alone, under 15 child plus parent (CNIL, via search summary). Minimize data, pseudonymous id, EU hosting, processing agreements with cloud and AI providers, no raw chat logs, child-readable privacy notice, delete and export buttons, impact assessment at scale. Not needed for a demo with test values; the design still shows the intent.

## 10. Open questions for brainstorm and planning
- Who reviews the bricks and the fact sheet for correctness?
- Which two or three bricks give the best VR-vs-PC contrast in a recorded demo?
- What is the gamification frame that survives beyond one session?
- What does the AI actually add that rule-based adaptive difficulty cannot (free-text questions, error explanations in context)? Make this visible in the demo.

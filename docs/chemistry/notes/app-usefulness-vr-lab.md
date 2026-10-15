# Usefulness of the VR teacher lab kit

Date: 2026-10-15

## Summary
The idea is partly solid and narrower than the brainstorm suggests. The real value is safe rehearsal of a dangerous or costly step, not replacing a lab. As a portfolio proof of concept it is defensible if pitched as pre-lab safety and procedure rehearsal with teacher-parametrized variants.

## Key points
- **Judgment (holds up):** Safe failure of a hazardous step has real value; acid accidents happen (poor dilution technique, rushed work). Best audience: pre-lab rehearsal for first-year university and vocational students.
- **Judgment (challenge 1):** Teachers rarely have time to customize per student. Real labs already give each student a different unknown concentration, so parametrizing a standard experiment is more believable than inventing experiments.
- **Judgment (challenge 2):** Free-text authoring promises more than the catalog can deliver; a wrong hazardous experiment is a liability for a teacher. Catalog, rules and review mitigate this.
- **Judgment (challenge 3):** No learning advantage of VR over a simple simulation for concepts; VR only pays off if embodied procedure (order, handling, pouring) is the lesson.
- **Judgment (challenge 4):** A free browser simulation (PhET style) needs no headset. The edge must be the consequence moment and AI-composed variants.
- **Fact:** Add acid slowly to water, never the reverse. Dilution releases heat and can spatter or boil; concentrated acid is the most dangerous case. Use a lower concentration or a less hazardous heat-of-mixing example for a school-level demo, validated by a real teacher.

## Chemistry area for a small proof of concept (judgment)
| Area | Fit | Why |
|---|---|---|
| Inorganic / general bench (dilution, acid-base, neutralization) | Best | Simple rules (heat of mixing, pH, thresholds); taught at all levels; visible mistakes |
| Analytical (titration) | Good | Taught everywhere; rule-light; classic mistake is overshooting the endpoint (costly, not dangerous); per-student unknowns are real practice |
| Organic | Poor | Multi-step syntheses, mechanisms, reflux, solvents |
| Physical / instrumental | Poor | Needs instrument models |

## Owner clarification (2026-10-15)
The goal is pre-lab rehearsal, not replacing the lab.

## VR vs a traditional virtual lab for pre-lab work
- **Fact (verified):** Virtual and hands-on labs give similar conceptual scores, so a desktop virtual lab already does the conceptual job. Quest 2 chemistry apps felt awkward to students (Maribor 2024). VR barriers: cost, teacher training, few long-term studies (DCU).
- **Unverified (from memory):** studies of VR lab simulations report more presence and motivation but no more learning, possibly from cognitive load. Needs a search before it is relied on.
- **Judgment:** pre-lab work is usually done before class, often at home, where students have no headset. A Quest-only app misses the main pre-lab scenario. In class, 30 students need many headsets plus setup time.
- **Judgment:** VR is justified only where embodied procedure and the memorable consequence are the lesson (for example acid dilution). That is a narrow niche.
- **Judgment:** the architecture already has a playable PC preview (ADR-010). A PC or browser pre-lab as the main access path, with VR as an optional immersive mode, fits the evidence better. VR remains a legitimate portfolio showcase, but that is the owner's goal, not a teacher need, and should be said openly.

## AI-generated vs premade experiments
- **Premade wins on:** teacher trust (reviewed content), curriculum alignment, chemical correctness checked once, and speed. *Practice, not verified:* PhET and Labster work this way.
- **AI adds value for:** free-text group constraints (for example "no strong acids, mixed level, hints in French"), writing hints and feedback at the student's language and level, and mapping a teacher's intent onto the catalog.
- **Judgment:** varying numbers per student (unknown concentration, volume, difficulty) is better done with a form or sliders: faster, deterministic, cheaper, no hallucination. AI is justified only for free-text constraints and hint text.
- **Judgment:** safest design is vetted templates with the AI filling allowed slots (parameters, hints, group rules), never inventing chemistry. This is close to ADR-004. Composing an experiment from scratch is the riskiest and least useful for real teachers, but the best portfolio showcase.

## Recommendation (judgment)
1. Pitch as pre-lab rehearsal supporting PC and VR, PC as the main access path.
2. Vetted templates adapted by the AI through constrained slots.
3. VR as the immersive mode for one or two procedure-and-consequence experiments, such as acid dilution.

## Use cases for the app
- Pre-lab rehearsal; safe failure of a hazardous step; per-student parameter variants.

## Sources (accessed 2026-10-15)
See `learning-and-practice-overview.md`.

## Open questions
- Where do students do the pre-lab (home, school computer room, class)? Decides whether VR can work at all.
- Is the VR/AI portfolio showcase or teacher usefulness the priority? Leads to different scopes.
- Would a real teacher trust AI-adapted templates?
- Search to verify VR vs desktop virtual lab studies.
- Acid dilution vs titration as the first experiment: compare hazards, misconceptions, age level.
- Target curriculum and level; teacher review of the first experiment.

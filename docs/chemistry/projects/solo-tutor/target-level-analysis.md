# Target level deep dive: collège (cycle 4) vs lycée (seconde, short look at première/terminale spé)

Date: 2026-10-15. Context: AI + VR/PC solo practice concept (see `initial-assessment-college.md`). Owner wants VR, gamification and AI tutoring weighted EQUALLY, a VR version (school headsets) and a PC version (home), and a cloud pseudonymous profile that follows the student.

## Summary
- Fact: collège is mostly qualitative (particles, mass, mixtures, pH, "atoms are rearranged"). Seconde turns chemistry into calculations (dilution, mole, balancing equations, limiting reagent).
- Judgment: with the three pillars weighted equally, **seconde is the stronger primary target**. The decisive reason is the AI tutor: seconde errors are multi-step calculations that code can check and classify, so the AI has a real job. Collège wins on gamification and on "wow" particle visuals.
- Judgment: a "bridge" is useful as a **prerequisite layer inside a seconde product** (3e skills as an entry diagnostic), not as a second audience.
- This conflicts with the earlier README target (collège). It is a recommendation, not a decision; the owner chooses.
- Evidence is thin on: VR hardware counts, market size, and real classroom misconceptions at seconde. See "What I did not verify".

## 1. What students actually learn (and what I read)

### Collège cycle 4 (5e, 4e, 3e)
Read in full: Éduscol resource "Organisation et transformations de la matière", March 2016, 11 pages. It is an EXAMPLE progression ("n'a pas vocation à être modélisant"); teachers choose their own order, so any app must map to skills, not to a school year.
- 5e (example): states of matter, mass is conserved in a change of state, temperature stays constant for a pure substance, mass-volume proportionality, mixtures and aqueous solutions, solubility/miscibility (introduced), combustion as a chemical transformation, physical vs chemical change, first pH measurement, CO2 test with limewater.
- 4e: first particle model (molecules, atoms, ions) for states and changes of state, density (as a proportionality coefficient), solubility depends on substance and temperature, a chemical transformation = atoms rearranged, acid/base linked to H+ and OH-, periodic table as a lookup tool.
- 3e: reaction equation (students must INTERPRET a given equation in terms of reactants, products, atoms conserved; the text says they do not yet write and balance them), atom constituents, symbols, formulas of O2, H2, N2, H2O, CO2, m = rho x V, acid-base and acid-metal reactions.
- Official hook (fact): the resource recommends a diagnostic evaluation at the start (can be a digital form) and says microscopic models "se prêtent particulièrement à l'utilisation de logiciel de simulation".
- Note vs earlier notes: in this example progression pH measurement starts in 5e (acid-base reactions are 3e), and mass conservation in a CHEMICAL transformation is listed in 3e, while mass conservation in a state change is 5e. My earlier notes put "pH 3e" and "mass conservation 5e" too simply.
- Not read: the current official programme text (BO 2020 version). The earlier note used a copy only.

### Seconde générale et technologique
Read in full: official annex, 13 pages, ministry-hosted PDF (2019 programme; I did not check later amendments). Secondary source for hours only: 3 h/week physics-chemistry (cours-thales.fr, not official).
- Macroscopic: pure substances vs mixtures; identify a species from melting/boiling temperature, density or chemical tests (water, H2, O2, CO2); thin-layer chromatography; mass composition of a mixture; air composition; solvent/solute; **mass concentration in g/L**; maximum concentration; **prepare a solution by dissolution or dilution, choose the right glassware**; calibration ("dosage par étalonnage", colour scale or density).
- Microscopic: size and mass of atom vs nucleus, Z and A notation, electron configuration up to 3p (1s, 2s, 2p, 3s, 3p), valence electrons, noble gases, listed monoatomic ions (H+, Na+, K+, Ca2+, Mg2+, Cl-, F-), Lewis diagrams (given and interpreted), **definition of the mole** and counting entities / amount of substance from a sample mass (Avogadro number in the text).
- Transformations: write the equation for a state change; endo/exothermic; **write and balance reaction equations; spectator species; stoichiometry; limiting reagent**; modelled cases: carbon and methane combustion, acid on a metal, acid on limestone, hydrochloric acid on sodium hydroxide; synthesis with reflux and TLC; nuclear: isotopes, symbolic equation only.
- Fact: molar mass and concentration in mol/L are NOT in seconde; they arrive in première (see below).
- Official hooks (fact): the programme text asks teachers to "favoriser l'acquisition d'automatismes" and to give "temps de travail personnel ... dans et hors la classe", and lists "mettre en œuvre un protocole expérimental en respectant les règles de sécurité". The cycle 4 notions are re-listed as prerequisites in each seconde section, which supports a diagnostic layer.
- Also in seconde: mechanics, waves, electricity (out of scope for chemistry), Python recommended.

### Première and terminale spécialité (short)
- Première spé: I read a DRAFT ("PROJET", version 1, hosted by SNES), not the final text. Draft content: molar mass, molar volume, mol/L, Beer-Lambert spectrophotometry, redox and half-equations, **tableau d'avancement** (reaction progress table), colour titration and equivalence, Lewis written by students, polarity, hydrogen bonds, solubility, extraction, first organic chemistry, yield, combustion energy.
- Terminale spé: NOT read from an official text. Search snippets only: pH-metric/conductimetric titration, kinetics (half-life, first order), acid-base modelling, spontaneous evolution of a system. Treat as unverified.
- Judgment: première/terminale spé are the ones with a strong bac exam pull, but they are a smaller, more specialised group and need harder chemistry (equilibrium, titration curves). Too big for a solo portfolio.

### Documented struggles by level
- Collège (see `../../notes/college-student-struggles.md`): macro-to-particle link, particles given material properties ("sugar particles melt"), dissolving "it disappears" and mass, open vs closed system. Mostly abstracts and RSC summaries.
- Seconde and after (search snippets only, not full papers): the mole/amount of substance is repeatedly named the hardest notion by teachers (Ducamp et al. communication; Revue hybride de l'éducation 2025; Furió et al. 2002 review). Students mix up mass, mole and amount of substance, and apply formulas as algorithms without understanding. A small lycée report (3 of 19 students could correctly use a progress table a year after learning it; very small sample). Course notes stress two dilution ideas students confuse: the sample taken keeps its concentration, and the amount of solute is conserved during dilution. A Société chimique de France text reports rote use of n = m/M and similar formulas.
- Judgment: both levels have a "concept behind the numbers" problem, which suits a predict-then-reveal tutor. At seconde the app can catch it by checking steps, at collège only by checking a final choice.

## 2. Side-by-side against the pillars

Scores are 1 (poor) to 5 (strong), my judgment, not measured.

| Criterion | Collège (5e-3e) | Seconde |
|---|---|---|
| VR value (what VR adds over an animation or PC) | 3. Walking inside a flask and grabbing atoms is attractive, but a zoom animation teaches the same; no study shows VR is better at this age | 3-4. Glassware choice, pipetting, reading a meniscus, and building molecules are bodily/spatial skills the programme asks for; rehearsing before a real practical session is plausible value. Mole and stoichiometry calculations gain nothing from VR |
| Gamification potential | 4. Sorting, building, "predict then see", detective cases, collecting; natural fit for 11-15 | 3. Fictions like "lab technician orders" with generated cases work, but calculation loops risk becoming a worksheet with points |
| AI-tutor value | 2-3. Qualitative, mostly closed choices; AI mostly rephrases an explanation. Free-text explanations cannot be checked by code | 4. Multi-step numbers: code can recompute with typical wrong rules (forgot mL to L, swapped ratio, used density instead of concentration) and label the error; AI then explains and picks the next brick |
| Share of useful bricks that code can verify | About 70-80%: closed-choice rules (sorting, particle picture, atom counts) | About 90%: numeric answers with tolerance, equation balancing, limiting reagent, Lewis octet rule |
| GDPR / consent (age 15) | Most players are under 15: CNIL says consent must be given jointly by the child and a parent. A cloud profile needs a parent-consent flow | Most (not all) are 15 or older at some point in the year, so many can consent alone. Still not a blanket "digital majority" (CNIL view as relayed by a legal analysis) |
| School/AI rules (fact, via press relay) | National AI framework (14 June 2025): pedagogical use of generative AI allowed from 4e, only in class and supervised; AI micro-training on Pix compulsory in 4e and 2de. Home use by a collégien is not covered by that school framework | Same framework: AI use is more open in lycée (one source: "autonomous within an explicit learning framework"; the other said no separate lycée rule). Unclear, verify |
| Teacher/school adoption | Teachers have free ordering over 3 years, so the app must be skill-based. Official text endorses diagnostics and microscopic simulations | One common programme; text endorses automatismes and out-of-class work. Teachers are time-pressed (3 h/week for all physics-chemistry), so tiny, checkable homework items win |
| VR hardware by age | Consumer Quest: ages 10-12 need parent-managed accounts (Nov 2024 guide), 13+ own account; 6e-5e students straddle this. No national headset count found; regional example: Bourgogne-Franche-Comté 2022, 550+ headsets in 74 volunteer sites (50 collèges, 19 lycées, 3 CIO, 2 EREA) | All students 13+. Same lack of national data. School-managed devices may follow other rules (unverified) |
| Need for at-home practice | Moderate. Homework is lighter, content less drill-based | Higher (judgment): chemistry becomes calculation-heavy and "automatismes" are taught; no market data found, so this is an informed guess |
| Build complexity (solo dev) | Rules are easy; the cost is art and animation (particle views, believable visuals). Safe-content burden is low | Visuals are simpler; the cost is rules and data (formulas, ions, equations) and checking chemistry correctness. A non-chemist needs a teacher to review the bricks |
| Equal-weight total (VR + gamification + AI) | about 9-10 of 15 | about 10-11 of 15 |

Reading the table (judgment): the totals are close. What separates them is that AI value and consent friction both lean to seconde, while gamification leans to collège.

## 3. Exercise / gameplay ideas that work on all three pillars

"V" = code-verifiable. "VR add" = what VR gives that a PC cannot. All use stylised, non-imitable content; no real mixing instructions or quantities.

### Collège
1. **Particle zoom, predict first.** Pick the particle picture for a scenario (sugar dissolving, ice melting, water boiling), then watch it. V: yes (rule table per substance and state). VR add: stand inside the flask and see particles at scale. Gamification: streaks, unlock new scenarios. AI: targets the misconception tag missed ("particles of sugar do not melt").
2. **Is the scale lying?** Predict the balance reading for dissolving or a reaction in an open vs closed flask. V: yes (arithmetic and open/closed flag). VR add: little; PC is best. Gamification: detective cases. AI: names the specific slip ("you forgot the gas left the flask").
3. **Atom shuffle.** Rearrange atoms from reactants into products so counts match (interpret, not write). V: yes (atom counting). VR add: strong, grabbing 3D atoms. Gamification: star ratings by moves. AI: hints from the count difference.
4. **Mystery mixture mission.** Choose filtration, decantation, evaporation or distillation from properties (soluble? boiling point?). V: yes. VR add: moderate (procedure rehearsal). Gamification: missions. AI: explains the property that decided it.
5. **Float or sink cargo loader.** Predict flotation and compute mass from volume with m = rho x V under a ship limit. V: yes. VR add: moderate (pour layered liquids). Gamification: resource-management puzzle. AI: spots proportionality errors.
6. **pH detective (stylised).** Sort everyday liquids by predicted pH, then an acid/base neutralisation slider. V: yes. VR add: low. Gamification: sorting rounds. Safety: say clearly that real mixing is for the lab only.

### Seconde
1. **Dilution bench (hero VR brick).** Order: "make 100 mL at X g/L from this stock". Choose glassware, compute the volume to take, simulate pipetting and filling to the mark. V: yes (numbers, glassware choice, step order). VR add: strong, real hand and eye rehearsal before a practical session. Gamification: client orders with accuracy and speed. AI: classifies errors (unit slip, mixed up density with concentration, wrong glassware).
2. **Mole as "counting by weighing".** From a sample mass and formula, find number of entities and amount in mol; visual zoom from grams to 6.02e23. V: yes. VR add: low-moderate (scale zoom). Gamification: factory counter with levels. AI: step-by-step diagnosis, the most valuable AI use (mole is the named pain point).
3. **Reactor chef: balance, then limiting reagent.** Start with small particle counts (for example 3 CH4 and 5 O2), balance, find what runs out, show final contents; later move to amounts in mol. V: yes (stoichiometry solver; balancing is a deterministic algorithm). VR add: moderate (build molecules, watch consumption). Gamification: production line to optimise. AI: picks difficulty from a skill graph.
4. **Mystery concentration (calibration).** Match a colour-scale or density against standards to estimate an unknown. V: yes within a tolerance. VR add: moderate (rack of tubes). Gamification: forensic or food-inspector cases. AI: talks about uncertainty and tolerance.
5. **Lewis and ion builder.** Place valence electrons to satisfy octets (Z up to 18), name the listed ions, check formulas by electroneutrality. V: yes. VR add: moderate-strong (3D grab). Gamification: puzzle packs. AI: hints from valence count.
6. **Identify the unknown.** Use melting point, density and a test bank to identify a species. V: yes (lookup). VR add: moderate. Gamification: case files. Safety: show tests (for example limewater for CO2) as stylised, no steps to imitate; the hydrogen "pop" test and acid-on-metal stay on-screen only.

## 4. Recommendation (judgment) and risks

Recommended path
1. **Primary target: seconde.** Strongest AI pillar, highest share of code-verified content, least consent friction, a real at-home need, and a VR hero brick (dilution bench) that is tied to a programme line.
2. **A "bridge" layer, not a second audience.** At start, a 10-15 question diagnostic of 3e prerequisites (particle picture, atom counts, formulas O2/H2/N2/H2O/CO2, density, solubility, pH). It places the student on a skill graph: particles, atoms, formulas, mole, balancing, limiting reagent, dilution. This matches the seconde text, which restates collège notions as prerequisites, and gives the AI a clean "adjust difficulty" story.
3. **Demo slice (about 4 brick families):** dilution bench (VR hero plus PC), reactor chef (PC plus VR), mole counting (PC), particle zoom as diagnostic/bridge (VR plus PC). Same brick, same seed, same checker on both platforms; the cloud profile stores only brick id, seed, answer, error tag.
4. **VR test for every brick:** "what does VR add over the PC version?" If the answer is nothing, ship it PC-only and say so honestly.
5. **Switch to collège if:** you can reach a collège teacher but not a seconde one, you want the "walk inside the particles" showcase, or you refuse a parent-consent flow only because you plan real minors, not a demo. Then use the collège list above.

Risks of this recommendation
- Seconde content is calculation-heavy; the product can feel like a worksheet. Mitigation: orders/fiction and VR only where the body matters.
- Correctness burden is higher (equations, ions, electron configurations). A non-chemist must have every brick and rule table reviewed by a teacher.
- Hazard content in the programme (acid on metal, HCl with NaOH, methane combustion): keep virtual, no quantities or steps that can be copied; rule to show: add acid to water, never the reverse.
- Seconde teachers are time-pressed and bound to textbooks; adoption may need alignment to a specific manual. Unverified.
- Competing homework platforms likely exist at seconde (not researched).
- The programme date is 2019; later amendments not checked. The première spé source was a draft; terminale not read.
- Equal weighting of three pillars is a design cost: each pillar needs polish; solo-dev scope creep is the main danger.
- AI and minors: the national framework is a school framework; a home AI tutor for under-15s is a grey zone. EU AI Act classes AI that evaluates learning or steers it as high-risk (from my knowledge of Annex III, not confirmed by search); secondary sources say the dates moved to 2 Dec 2027 but I could not confirm publication in the Official Journal. Irrelevant for a demo, relevant before real use. Not legal advice.

## What I did not verify
- Official text of terminale spé and of the current cycle 4 programme.
- National VR headset counts per level; real adoption of PhET/Labster/ChemCollective in France (searches returned only product descriptions).
- Market size for at-home practice (nothing found).
- CNIL pseudonymisation guidance for EdTech; whether school-contracted use uses a legal basis other than consent (only a secondary blog said: public-interest mission).
- Meta rules for school-managed headsets.
- Official AI-framework page (403 error); relied on a Localtis article (19 June 2025) and search snippets from other relays.
- Seconde misconception papers (snippets only).

## Questions for the owner
1. Is your real audience seconde teachers, collège teachers, or hiring managers looking at a portfolio? It changes whether you optimise for classroom fit or for wow.
2. Can you get 20 minutes with one seconde and one collège physique-chimie teacher to check the dilution bench and the 3e diagnostic?
3. Will the demo use real minors' data at any point, or only test accounts? That decides if the consent flow gets built.

## Sources (accessed 2026-10-15)
Read in full:
- https://eduscol.education.gouv.fr/sites/default/files/document/ra16c4phchmatiereprogression680433pdf-78105.pdf (Éduscol, March 2016, cycle 4 progression example)
- https://cache.media.education.gouv.fr/file/SP1-MEN-22-1-2019/98/9/spe634_annexe_1062989.pdf (seconde programme annex)
- https://www.snes.edu/IMG/pdf/arrete_physique_spe_1eg_ensemble.pdf (première spé DRAFT, "PROJET" v1)
Fetched, partial or secondary:
- https://www.cours-thales.fr/seconde/programme-physique-chimie (3 h/week; secondary)
- https://www.banquedesterritoires.fr/ia-en-education-ce-que-prevoit-le-cadre-dusage-pour-la-communaute-educative (Localtis, 19 June 2025)
Search snippets only (not read in full):
- https://cnil.fr/fr/la-cnil-publie-8-recommandations-pour-renforcer-la-protection-des-mineurs-en-ligne (CNIL, consent under 15)
- https://connectsafely.org/quest-kids/ (Meta parent-managed accounts, Nov 2024)
- https://www.banquedesterritoires.fr/orientation-bourgogne-franche-comte-plonge-ses-eleves-dans-la-realite-virtuelle (headsets, 2022)
- https://www.gibsondunn.com/eu-ai-act-omnibus-agreement-postponed-high-risk-deadlines-and-other-key-changes/ (AI Act dates, May 2026)
- https://pubs.rsc.org/en/content/articlehtml/2002/rp/b2rp90023h (Furió et al., mole review)
- https://new.societechimiquedefrance.fr/jirec2020_communication_ducamp (Ducamp, mole difficulty)
- https://revues.uqac.ca/index.php/rhe/article/download/1785/1674/5317 (Revue hybride de l'éducation, 2025)
- https://dumas.ccsd.cnrs.fr/dumas-04826515v1/document (small lycée study, progress table)
- https://www.clubic.com/actualite-568980-ca-y-est-l-intelligence-artificielle-generative-entre-dans-les-classes-francaises-avec-des-regles-les-voici.html (AI framework press relay)

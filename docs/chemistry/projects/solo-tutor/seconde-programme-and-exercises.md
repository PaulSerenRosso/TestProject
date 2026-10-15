# Seconde chemistry: programme, exercise types, exam formats, gamification hooks

Date: 2026-10-15. Project: solo-tutor (see `concept.md`). Purpose: one reference the owner and the game-design work can read to see **what a French seconde student learns in chemistry, what exercises they really get, and which exercise shapes can become game bricks**.
Tags: **[fact]** = read in a source below. **[practice]** = varies by teacher/school or seen in a few documents only. **[judgment]** = my opinion or my own chemistry knowledge, not sourced.
Scope: chemistry only ("Constitution et transformations de la matière"). Mechanics, waves and electricity are out of scope.

## 1. Summary
- [fact] Seconde générale et technologique, programme of 2019 (I did not check later amendments). The chemistry theme has 2 big parts: (1) matter from macroscopic to microscopic scale, (2) modelling transformations and energy transfer.
- [fact] The official text lists **no order**: the teacher chooses the progression. It asks for "automatismes" and personal work "dans et hors la classe".
- [fact] The only concentration in the text is **mass concentration in g/L**. **Molar mass and mol/L are not listed** (they are première). The mole is introduced by counting entities (N = m / mass of one entity, n = N / NA).
- [practice] Real worksheets drift beyond this: a popular free site labels mol/L and molar-mass exercises "2nde". For a tutor that must match the programme, treat mol/L as out of scope unless a teacher says otherwise.
- [judgment] Most seconde chemistry exercises are **short numeric or choice tasks with one right answer plus a justification**, which suits code-checked bricks. The hard-to-gamify part is the written justification and the real hands-on technique.

## 2. Programme map (what is taught)
Source: official annex (Ministry PDF). Each row = a capacity the student must show. "Brick-able" = a code checker can mark it (my judgment).

### A. Matter at the macroscopic scale
| Notion | What students must do [fact] | Brick-able? |
|---|---|---|
| Pure substance vs mixture, homogeneous vs heterogeneous | Give everyday examples; tell a mixture from a pure substance using experimental data | Yes (sorting, data tables) |
| Identify a chemical species | Use reference values (change-of-state temperatures, density) or chemical tests; know common tests for water, dihydrogen, dioxygen, carbon dioxide | Yes (lookup/elimination). Tests stay on-screen only |
| Composition of a mixture, air | Mass composition; air approx. composition and density order of magnitude; use percentages and fractions | Yes |
| Density vs mass concentration | Water density and comparison; **explicitly "distinguish density from mass concentration"** | Yes. This is an official confusion hook |
| Solutions: solvent, solute | Identify solute and solvent from a composition or a preparation method | Yes |
| Mass concentration (g/L), maximum concentration | Compute Cm = m / V; rearrange the quotient for numerator or denominator; compute from a preparation by dissolution or dilution; find a maximum concentration from results | Yes (numbers, units) |
| Preparing a solution | Choose and use the right glassware for dissolution or dilution; measure masses to study the variability of a glassware volume | Partly (choice and order: yes; hand technique: VR only) |
| Calibration ("dosage par étalonnage") | Find a concentration from a calibration range (colour scale or density measurement) | Yes within a tolerance |
| Chromatography (TLC), tests | Run a TLC and tests to identify a species and say if the sample is a mixture | Reading a chromatogram: yes |

### B. Matter at the microscopic scale
| Notion | What students must do [fact] | Brick-able? |
|---|---|---|
| Species as a collection of identical entities; molecular vs ionic species; electroneutrality | Use electroneutrality to pair ions and cite ionic compound formulas | Yes |
| Entities | Name a given formula "molecule, atom, anion or cation" | Yes |
| Atom and nucleus | Order of magnitude of atom size; compare size and mass of atom and nucleus; use powers of 10 and scientific notation | Yes |
| Z, A, notation of a nucleus | Write the notation of a nucleus from its composition and the reverse | Yes |
| Electron configuration (1s, 2s, 2p, 3s, 3p), periodic table (s and p blocks) | Place an element from its configuration; find valence electrons (Z up to 18); chemical families, noble gases | Yes |
| Stability, monoatomic ions | Link stability to the noble-gas valence configuration; find the charge of common ions; **name H+, Na+, K+, Ca2+, Mg2+, Cl-, F-** and write formulas from names | Yes |
| Lewis model | Read and use a given Lewis diagram to justify stability (Z up to 18); bond energy qualitatively. In seconde Lewis diagrams are **given and interpreted** | Yes (octet/duet check) |
| Mass of an entity | From the formula and the masses of the atoms | Yes |
| Counting entities, the mole | Find the number of entities and the amount in mol in a sample mass; mole = 6.022 140 76 x 10^23 entities | Yes. Named the hardest notion by teachers (see section 5) |

### C. Transformations
| Notion | What students must do [fact] | Brick-able? |
|---|---|---|
| Physical transformation | Write the equation of a change of state; tell fusion from dissolution; endothermic vs exothermic; use the energy of change of state (E = m x specific energy) | Yes |
| Chemical transformation | From data, model by a reaction, write and **balance** the equation; **spectator species**; **stoichiometry**; **limiting reagent** (from amounts, or from the final state) | Yes (balancing is deterministic) |
| Named modelled cases | Equations for combustion of carbon and methane, corrosion of a metal by an acid, acid on limestone, hydrochloric acid with sodium hydroxide | Yes, on-screen only (no real procedure) |
| Energy | Follow a temperature to decide endo/exothermic and study the effect of the limiting reagent mass | Partly |
| Synthesis | Draw a labelled reflux set-up and a TLC; run a reflux synthesis; compare a synthesised and a natural species by TLC | Drawing/labelling: yes. Real synthesis: no |
| Nuclear | Isotopes; Sun and power plant linked to nuclear reactions; tell physical, chemical or nuclear from a description or equation | Yes (sorting) |

### D. Cross-cutting [fact]
- Competences used to structure teaching and evaluation: **S'approprier, Analyser/Raisonner, Réaliser, Valider, Communiquer** (2019 annex, with example capacities such as "choose a model", "write a protocol", "carry out routine calculations", "critical spirit and plausibility tests", "present an argued approach").
- "Mesure et incertitudes": histogram, mean and standard deviation of repeated measures, significant figures, qualitative comparison with a reference value. Relevant to every practical.
- Python is the recommended language; the programme also recommends modelling and simulation.
- Safety is part of "Réaliser" ("mettre en œuvre un protocole en respectant les règles de sécurité").
- Prerequisites from collège are re-listed at the top of each section: species, pure substances/mixtures, air, density, states of matter, solubility, miscibility, molecules/atoms/ions, atom constituents, formulas O2, H2, N2, H2O, CO2; mass conservation, redistribution of atoms, equation notion, acid-base reactions, acid on metal, pH. This supports the diagnostic layer in `concept.md`.

## 3. How a year can be organised
- [practice] One real teacher progression (Académie de Guyane, 2019/20, 7 pages) puts chemistry first: identify species (change-of-state temperature, density, tests, TLC); glassware and solutions; "dosage cola / light" and **échelle de teinte**; then atoms, ions and the periodic table; then the mole; then energy of change of state; then reactions, balancing and limiting reagent; then synthesis with reflux and TLC; nuclear last. Mechanics, optics, sound and electricity follow in the same year. The order is the teacher's choice, so do not hard-code it.
- [practice] Typical weekly rhythm: lesson, "activité", and a TP (practical). One source speaks of "RPS", which I did not find defined; likely "résolution de problème scientifique" (judgment).
- [fact, secondary source] 3 h per week for all of physics-chemistry (cours-thales.fr, not official).

## 4. Exercise types seen in real material
Evidence: real seconde-level worksheets and exercise banks (sources at the end). I found **no complete real seconde DS (controlled test) with solutions**, so the exam section below mixes sourced facts with my knowledge of common practice.

### 4.1 Catalogue by notion (real or realistic; numbers are examples)
| # | Notion | Exercise shape | Example (paraphrased) | Answer format | Code-checkable |
|---|---|---|---|---|---|
| E1 | Dilution | Calculate + glassware + order the steps | From a stock at 0.5 g/L make 500 mL at 0.01 g/L: dilution factor F = Cmother / Cdaughter = 50; volume to take = 500 / 50 = 10 mL; glassware = beaker, 10.0 mL volumetric pipette, 500.0 mL volumetric flask. A drawing-ordering sub-question asks to put the stages in order [fact: school workbook] | Number + unit, choice, ordered list | Yes |
| E2 | Dilution | Guided problem | Daughter solution 100 mL from a 1-in-20 dilution: 100.0 mL flask and 5.0 mL pipette [fact: Académie de Versailles resource, via search summary] | Number, choice | Yes |
| E3 | Dissolution | Compute concentration, then required mass | 0.50 g dissolved in a 100.0 mL flask gives Cm = 5.0 g/L; to make 200 mL at 0.01 g/L weigh 0.0020 g (2 mg) [fact: same workbook]. It also imposes a **4-step answer layout**: sentence naming the quantity, formula with units, the operation, boxed result with unit | Number + unit, plus layout | Number: yes. Layout: partly (can be a form with 4 fields) |
| E4 | Dilution | MCQ | "Compute a dilution factor", "compute the volume to take" (Kartable, 2nde) [fact, via search summary] | Choice | Yes |
| E5 | Calibration | Read a unknown on a colour scale or a density curve | Match a sample tube to standards (échelle de teinte); estimate concentration | Number in a tolerance, or tube choice | Yes within tolerance |
| E6 | Mole / counting | Convert N and n | 0.50 mol of Cu atoms -> N = 3.0 x 10^23 atoms; 1.806 x 10^25 Sn atoms -> n = 30 mol, with NA given as 6.02 x 10^23 mol-1 and n = N / NA given [fact: workbook] | Number in scientific notation + unit | Yes |
| E7 | Mole / mass of an entity | Several steps | Mass of one entity from atom masses given in kg, number of ions from a sample mass, then amounts in mol; ions produced by a dissolution equation [fact: workbook, but see the note below on its numbers] | Numbers | Yes |
| E8 | Atom, nucleus | Tick the correct statement | "Isotopes have the same number of protons and a different number of neutrons" [fact: workbook] | Choice | Yes |
| E9 | Lewis | Pick the right diagram and justify; spot molecules that break octet/duet | Methanoic acid HCOOH: circle the correct Lewis representation and argue; circle molecules not respecting octet/duet [fact: workbook] | Choice + short justification | Choice: yes. Justification: no (but can be a pick-the-reason list) |
| E10 | Balancing | Balance equations | A set of given unbalanced equations (content is images in the source; the topic is fact) | Coefficients | Yes |
| E11 | Limiting reagent | Find the limiting reagent | From amounts and the equation (content is images in the source; topic is fact) | Species + amounts | Yes |
| E12 | Amount of substance (practice) | Mass <-> n with molar mass | Sucrose C12H22O11 and CuSO4: compute M, n in a 5.5 g sugar cube, mass of 0.5 mol [practice: exercise labelled 2nde on pass-education.fr, but molar mass is not in the 2019 text] | Number | Yes. **Off-programme risk** |
| E13 | Identify a species | Table lookup | Use melting temperature, density and test results to decide which species it is | Choice | Yes |
| E14 | Sorting | Mixture/pure, homogeneous/heterogeneous, physical/chemical/nuclear | Classify everyday cases or equations | Category | Yes |
| E15 | Temperature curve | Read a heating/cooling plot | Identify the plateau and say pure substance or mixture; endo or exothermic | Choice, number | Yes |
| E16 | Ions | Name and write | Name H+, Na+, K+, Ca2+, Mg2+, Cl-, F-; find an ion's charge from the periodic table; ionic formula by electroneutrality | Text/choice | Yes |
| E17 | Electron configuration | Fill and read | Write 1s/2s/2p/3s/3p for Z up to 18; valence electrons; position in the table | Configuration string | Yes |

Notes on the evidence:
- [judgment] The workbook's own text is inconsistent (title "sulfate de cuivre" vs text "sulfate de fer" in E3; E7 says 3.0 g of AlCl3 gives 1.35 x 10^25 Al3+ ions, but I get 1.35 x 10^22 for 3.0 g, which matches 3.0 kg or a typo). Real worksheets contain errors. This is a good argument for generating bricks from code with a checker rather than copying exercises.
- E1 and E3 together show the standard **prepare-a-solution family**: numbers, glassware, order of steps. This is the best-documented seconde exercise family I found.
- Not found in detail: real seconde exercises for balancing and limiting reagent (images in the sources), real DS papers, and real TP reports.

### 4.2 Question formats [practice]
- **Calculation with unit and justification** (most frequent in the material I saw). Marked on method, unit and significant figures.
- **MCQ / tick the right box**, sometimes with "justify".
- **Ordering** (put the steps of a dilution in order, from drawings).
- **Naming** (name the glassware, name the ion, name the entity: molecule/atom/anion/cation).
- **Drawing/labelling** (Lewis diagram, reflux set-up, TLC plate).
- **Sorting/classification** (physical vs chemical vs nuclear, pure vs mixture).
- **Graph/table reading** (cooling curve, calibration scale, density table).
- **Document-based problem** ("scorbut and vitamin C": a short text, then calculations) [practice: the context-text exercise format appears in the 2nde banks; its questions were not visible].
- **Written justification / short explanation** (Lewis, plausibility, reasoning).

## 5. Where seconde students go wrong (misconceptions and typical errors)
Evidence level is mixed: the mole and dilution points come from teacher/research summaries I saw only as snippets in earlier research (see `target-level-analysis.md`); the rest is my chemistry-teaching judgment and should be checked with a real teacher.
- [practice, snippets] The **mole** is the notion teachers name as hardest: students mix mass, number of entities and amount of substance, and apply formulas as recipes.
- [practice, snippets] **Dilution**: students confuse "the sample taken keeps its concentration" with "the amount of solute is conserved". Rote use of formulas.
- [fact] The programme itself targets one confusion: density vs mass concentration (both in g/L, different things).
- [judgment] Likely wrong rules to detect in code (good for error tags): forgot mL to L; inverted F (Cdaughter / Cmother); used the flask volume where the volume taken was needed (or the reverse); added a fixed volume of water instead of filling to the mark; used a measuring cylinder where a volumetric pipette is required; used solution mass instead of solute mass; power-of-10 slips with NA; used A instead of Z (or the reverse); counted valence electrons from the wrong shell; changed subscripts instead of coefficients when balancing; confused coefficient with subscript; picked the limiting reagent as the smaller **number** rather than the smaller amount **divided by its coefficient**; wrong ion charge.
- [judgment] Written justification is where the most marks are lost and the hardest thing to automate.

## 6. Exams, homework and in-class activities [practice unless noted]
No national exam at seconde. Format knowledge below is general practice; I found no complete sample paper, so treat durations and weights as unverified.
| Format | What it looks like | How a tutor app relates |
|---|---|---|
| **Questions flash / automatismes** | The official text asks for automatismes; a ministry resource reportedly recommends short regular questions (a snippet says 2-3 questions, under 10 min with correction) [fact via snippet, not read in full] | Best fit: a daily 2-3 brick warm-up |
| **Contrôle / DS** (written test in class) | Calculations, MCQ, Lewis, balancing, labelled drawings, with data tables supplied; often competences tagged (S'approprier, Analyser, Réaliser, Valider, Communiquer) | Practice with the same shapes; no real exam simulation claim |
| **DM** (homework) | Longer problems, document-based tasks | Fits tutor practice outside class |
| **TP / practical with write-up** | Prepare a solution, make a colour scale, TLC, identify a species; students write protocol, calculations and a conclusion; sometimes evaluated on technique | Pre-lab rehearsal (VR/PC); never a replacement of hands-on |
| **Evaluation diagnostique / vacation work** | Collège prerequisites checked at the start; a school gives a holiday workbook from seconde to première, with one exercise reused in a première test [fact: workbook text] | Matches the diagnostic bridge in `concept.md` |
| **Compétence-based grading** | Marks attached to S'approprier / Analyser / Réaliser / Valider / Communiquer rather than to topics alone [fact for the list; marking scheme is teacher-specific] | Brick tags can mirror these five |

## 7. From exercise shapes to game bricks (input for game design)
This is a bridge, not a design. The `game-design-expert` agent should own mechanics.

### 7.1 Shapes that suit a game
| Shape | Native exercises | Natural game mechanic (ideas) | VR value (judgment) |
|---|---|---|---|
| Numeric answer with unit + tolerance | E1, E3, E6, E7, E12 | Client orders, accuracy score, streaks | Low |
| Order the steps | E1 (dilution procedure) | Assemble the procedure; timer for speed bonus | High if hands-on (pipette, fill to mark) |
| Choose the tool | E1 glassware, E4, E5 | Equip the bench; wrong tool shows a visible error margin | Medium-high |
| Build/rearrange | E9, E10, E17 (atoms, electrons, coefficients) | Atom puzzles, assembly lines, "reactor" | Medium-high (3D grab) |
| Sort/classify | E14, E16, E13 | Fast sorting rounds, case files | Low |
| Read a scale/graph | E5, E15 | Detective or inspector cases | Medium |
| Pick the right diagram/reason | E8, E9 | Spot-the-mistake rounds | Low |
| Free-text justification | E9, E3 layout | Not auto-checkable; use a "pick the reason" list or the 4-step form | n/a |

### 7.2 Gamification hooks tied to official wording
- "Distinguish density from mass concentration": a mini-game where the same bottle shows both numbers and the player picks which one a recipe needs.
- "Choose and use the right glassware": a tool rack with precision stakes. A wrong tool gives a measurable error, using the programme's uncertainty ideas.
- "Identify the limiting reagent": a production line that stops when one input runs out.
- The 4-step answer layout (name the quantity, formula with units, operation, boxed result): a "report card" scored per step, worth points independently from the final number.
- Technician fiction (orders, quality control, lab inspector) fits calibration, identification and dilution; it does not fit Lewis or electron configuration, which are better as puzzles.
- [judgment] Keep a hard line between "game over" and "wrong chemistry": never reward a wrong rule, and show the error tag, not just "wrong".

### 7.3 What not to gamify (judgment)
- Real procedure steps for hazardous cases in the programme (acid on metal, HCl with NaOH, methane combustion): equations and results only. Safety rule to keep visible: **add acid to water, never the reverse**.
- Written scientific communication and real hand technique: say plainly that the app does not train them.
- Nuclear and the synthesis TP: low value for the demo.

### 7.4 Suggested priority for the demo slice (judgment)
1. Prepare-a-solution family (E1-E5): best-documented, official, VR-friendly, fully checkable.
2. Mole/counting (E6-E7): highest teacher-named pain, fully checkable, little VR value.
3. Balancing + limiting reagent (E10-E11): deterministic checker, strong game fit.
4. Lewis/ions (E8, E9, E16, E17): puzzle fit, clear rules.
5. Identification and sorting (E13-E15): cheap to build, good for warm-ups and the diagnostic.

## 8. Risks and what to check with a real teacher
- Programme version is 2019; amendments not checked. Textbook choice shapes what students actually see (mol/L, molar mass).
- The exercise evidence is thin on balancing, limiting reagent and DS papers: ask one seconde teacher for 3 real recent tests (even anonymised) and the five most common wrong answers.
- The official text calls for justification and protocol writing; a pure numeric app covers about half of what students are assessed on.
- Chemistry correctness: every brick, rule table and distractor must be reviewed by a teacher before any real use.

## Open questions
- Does the owner want molar mass and mol/L in a later layer (première bridge) or strictly stay with the 2019 seconde text?
- Can the owner get 2-3 real seconde chemistry tests, one TP write-up, and a common-mistakes list from a teacher?
- Which of the 5 competence tags (S'approprier ... Communiquer) should bricks carry for the teacher summary?
- Not verified: terminale and première official final texts (not needed here), real prevalence of mol/L in seconde textbooks.

## Sources (accessed 2026-10-15)
Read in full or extracted from the file:
- https://cache.media.education.gouv.fr/file/SP1-MEN-22-1-2019/98/9/spe634_annexe_1062989.pdf (official seconde annex, 2019; competences, repères, chemistry tables)
- https://physique-chimie.dis.ac-guyane.fr/IMG/pdf/progression_seconde.pdf (Académie de Guyane, teacher progression 2019/20; layout partly garbled in extraction)
- https://lyc-cassin-arpajon.ac-versailles.fr/IMG/pdf/cahiervacances_2ndevers1ere_2024_version_2.pdf (lycée holiday workbook, exercises 1-8 used above)
- https://phychim.ac-versailles.fr/IMG/pdf/progressivite__et_ressources_dilution_dosages.pdf (Versailles, dilution and calibration from 2nde to terminale; confirms mol/L is première)
- https://www.pass-education.fr/preparation-d-une-solution-aqueuse-2nde-exercices-corriges/ (exercises labelled 2nde that use mol/L: off-programme)
- https://www.pass-education.fr/determination-et-prelevement-de-la-quantite-de-la-matiere-2nde-exercices/ (molar-mass exercises labelled 2nde)
Search snippets only (not read in full):
- https://kartable.fr/ressources/physique-chimie/exercice/calculer-un-facteur-de-dilution/49965/140262.pdf and https://kartable.fr/ressources/physique-chimie/exercice/calculer-le-volume-a-prelever-pour-une-dilution/20390/132609.pdf (MCQ on dilution)
- https://eduscol.education.fr/document/24577/download and https://ent2d.ac-bordeaux.fr/disciplines/sciences-physiques/wp-content/uploads/sites/7/2020/03/Automatismes-Spécialité-Physique-Tale.pdf (automatismes, questions flash, MCQ formats; Terminale, transposed)
- https://www.cours-thales.fr/seconde/programme-physique-chimie (3 h per week, secondary)

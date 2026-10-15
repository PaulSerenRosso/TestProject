# Gamified learning reference: seconde (grade 10), mathematics and chemistry

Date: 2026-10-15. Status: Reference (durable, not a GDD). Owner: solo developer of the solo-tutor project.
Purpose: rules and guidelines to follow so that a gamified exercise or practice session actually works for a ~15-year-old seconde student in maths and in physique-chimie (chemistry part). Top-down: general rules (1), teenagers and the two subjects (2), what existing products teach us (3), application to the solo-tutor project (4).
Tags used (same convention as `docs/chemistry/`): **[fact]** = read in a source listed at the end; **[snippet]** = seen only in a search summary, not read in full; **[background]** = well-known literature I cite from memory, not re-checked in this session; **[judgment]** = my opinion or inference. Anything not tagged is a definition or a structural statement.
Scope warning: the solo-tutor project (as documented on 2026-10-15) covers **chemistry only**. Maths appears here because the owner asked for the reference; no maths content exists in the project docs.

---

## 0. One-page summary (read this if nothing else)

1. Gamification works **a little, on average, and unevenly** (small-to-medium effects, huge variation, weak research quality). It is a seasoning on good practice, not a substitute for it. [fact]
2. The practice itself must follow the learning-science basics: **retrieval, spacing, interleaving, immediate informative feedback, worked examples that fade, desirable difficulty**. These beat any badge. [fact/background]
3. Motivation: serve **competence, autonomy and relatedness** (self-determination theory). Points, badges and leaderboards are, at best, **progress feedback**; at worst, controlling pressure. Never rely on them as the reason to practise. [fact/background]
4. For teens: respect autonomy, avoid childish look and public comparison, keep sessions short, let them feel clever not tested. [judgment + background]
5. The best "game" at this level is a **meaningful task with a story** (client order, case file, production line) where the learning content IS the gameplay, not a quiz after a mini-game. [fact: fiction moderates effects; judgment]
6. Maths and chemistry differ: maths is abstract, procedural, hierarchical (fits adaptive mastery loops and puzzle-like mechanics); chemistry adds a **three-level representation problem** (macro, particle, symbol) and units/quantities (fits simulations, predict-then-reveal, and quantity-based tasks). [background + judgment]
7. Existing products show the same pattern: **engagement is easy, learning transfer is hard**. Products with the best evidence (Khan-style mastery practice, some DragonBox results, PhET) are simple, feedback-rich and tied to a curriculum; products with the loudest gamification (Prodigy, Duolingo) have the weakest independent learning evidence. [fact/snippet]
8. For solo-tutor: the architecture already has the right bones (code-checked answers, error tags, derived progression, seeded fallback). Biggest gaps: **no spaced/interleaved scheduling rule yet, no gamification frame (Q8), no learning measurement, streak/XP rules unspecified (risk of dark patterns)**. Section 4 lists concrete rules.

---

## 1. General rules of gamification and game-based learning

### 1.1 Definitions (one line each)
- **Gamification** = adding game elements (points, badges, levels, narrative) to a non-game learning task. **Game-based learning / serious game** = the learning content is the game itself. Solo-tutor aims at the second, with some of the first layered on.
- **Core loop** = the repeated cycle of action, feedback and reward. **Flow** = challenge matched to skill (Csikszentmihalyi). **Intrinsic motivation** = doing it for its own sake; **extrinsic** = doing it for a reward. **Overjustification effect** = an expected reward for an already-enjoyed activity can lower later interest in it.

### 1.2 What the evidence says about gamification as a whole
| Source | Result | Reading |
|---|---|---|
| Sailer and Homner 2020, meta-analysis | Small significant effects: cognitive g = .49 (k=19), motivational g = .36 (k=16), behavioural g = .25 (k=9). Cognitive result stable in rigorous studies; motivational and behavioural less stable. Game **fiction** and mixing competition with collaboration moderated behavioural effects [fact] | Works on average, modestly. Fiction (a story with roles) helps |
| Wouters et al. 2013, serious games | Learning d = 0.29 (77 studies), retention d = 0.36; **no motivational advantage** over conventional teaching (d = 0.26, not significant per summary). Games beat conventional teaching more when **combined with other instruction**, over **multiple sessions**, and in groups [snippet] | Games are not magically more motivating; they teach best as part of a course |
| Clark, Tanner-Smith, Killingsworth 2016 | Games vs non-game d = 0.33; augmented vs standard game design d = 0.34. Design matters; **simpler, schematic visuals matched or beat visually complex ones** [snippet] | Do not spend the budget on spectacle |
| Other 2020-2026 meta-analyses | Pooled g from ~0.46 up to above 0.8, one with I2 = 98.8% heterogeneity [snippet] | Large numbers come with huge heterogeneity and weak designs; do not quote them as promises |
- [judgment] Honest reading: gamification has a **positive but modest** average effect, a **very wide spread**, and published studies skew to short, small, motivated samples. Treat any single study (including those cited below) as a hint, not a law.

### 1.3 Motivation: self-determination theory (SDT)
- [background] Ryan and Deci (2000): lasting motivation needs three needs met: **competence** (I can do it, I see progress), **autonomy** (I choose, it is not forced), **relatedness** (I belong, I am not judged). Extrinsic motivation becomes durable only when internalised (the student sees the value).
- Design translation (judgment):
  | Need | Do | Don't |
  |---|---|---|
  | Competence | Visible mastery per skill, success rate that stays high enough, specific feedback | Streaks of failure shown as "you lost", red crosses with no explanation |
  | Autonomy | Choice of next topic or difficulty (within guardrails), optional challenges, skip/opt-out of gamified bits | Forced badges, forced daily streak, "you must do X to continue" |
  | Relatedness | Optional, private, supportive social features (share a recipe or a solved case), teacher or tutor voice that is warm | Public rankings of all students, shaming messages |

### 1.4 Rewards: points, badges, leaderboards, streaks
- [fact, meta-analysis] Deci, Koestner and Ryan (1999): across 128 studies, tangible, expected rewards (engagement-, completion- and performance-contingent) reduced later free-choice intrinsic motivation (d about -0.28 to -0.40). The result is **disputed** (Cameron and Pierce argued it is small); the debate is unresolved. [snippet]
- [snippet] Mekler et al. 2017 (points, levels, leaderboards on an image-annotation task): performance went up, but **no effect on competence or intrinsic motivation**. Reading: these elements act as **progress indicators that steer effort**, not as motivation builders.
- [snippet] Hanus and Fox 2015 (one 16-week course, 80 students, mandatory badges + leaderboard): gamified group ended with **lower motivation, satisfaction and exam grades**; authors blamed social comparison and lack of autonomy. One study, but a vivid warning. A later study found the opposite (Hazan 2018, via a table), so the evidence is mixed. [snippet]
- Practical rules (judgment, consistent with the above):
  1. Rewards should be **informational** ("you can now do 2-step dilutions"), not controlling ("do this to get coins").
  2. Reward **process and mastery** (using the right method, fixing an error, reaching a new level), not raw speed or volume.
  3. **Unexpected** or **skill-contingent** rewards are safer than a promised prize for doing anything.
  4. **No public leaderboard** among classmates. If any comparison exists: personal best, or anonymous/opt-in, never the bottom of a list visible to peers.
  5. Streaks: powerful for retention, **risky for learning and wellbeing** (Duolingo-style streaks are widely reported to produce "playing the game" behaviour and anxiety; evidence is commentary and a qualitative study, not an RCT [snippet]). If used, make them forgiving (weekly goals, freezes, no loss messaging) and never tie them to content access.
  6. Avoid **lives/hearts** that block practice: they punish exactly the students who need more practice.
  7. Watch for **gaming the system** (rapid guessing, hint-spamming, XP farming on easy items). Design the XP formula so farming easy items gives little.

### 1.5 Flow, difficulty and failure
- Flow needs clear goals, immediate feedback and a challenge near the edge of skill. Target for adaptive practice: **mostly successes with a stretch** (a common design target is roughly 70-85% success; this number is [judgment/background], not a hard law). Too easy = boredom, too hard = anxiety; a seconde student is very sensitive to the second.
- [background] **Desirable difficulties** (Bjork): effortful retrieval, spacing and interleaving feel harder and slower but produce better retention. A learner's feeling of fluency is a poor guide; do not optimise the app for "feels easy".
- [snippet] **Productive failure** (Kapur; Sinha and Kapur 2021 meta-analysis of 53 studies, mostly maths, physics, chemistry): attempting a problem **before** instruction, then being taught the canonical method and why the attempts fell short, can beat instruction-first for **conceptual** understanding. Caveats: effect sizes not retrieved; another source says some randomised studies found the opposite [snippet, unverified]. Use for concepts (mole, dilution idea), not for pure procedures.
- Failure must be **safe and informative**: a wrong answer is a data point labelled with its likely cause, not a punishment.

### 1.6 Feedback
- [snippet] Kluger and DeNisi 1996: on average feedback helps (d about .4), but **over a third of feedback interventions reduced performance**; critics note most studies were not in schools and measured performance, not learning. Message: feedback quality, not quantity.
- Rules (judgment + Hattie and Timperley's framework [background]):
  1. Say **what was wrong and why** (error type), **where to look** (the step), and **what to do next**; not just right/wrong.
  2. Feedback on the **task and process**, not on the person ("the unit conversion was missed", not "you are bad at this").
  3. **Immediate** for procedures, slightly **delayed or after an attempt** for concepts (let the student commit to a prediction first).
  4. Never praise a wrong method; never let a correct number with a wrong method pass silently.

### 1.7 Learning-science practice rules the game must embed
| Technique | Evidence | What it means for design |
|---|---|---|
| **Retrieval practice** (practice testing) | Dunlosky et al. 2013 rated practice testing and distributed practice **high utility**; rereading, highlighting, summarising low [snippet via press summary]. Roediger and Karpicke 2006 [background] | Make the student **produce** answers (type a number, build a molecule), not recognise from a list. Low-stakes, frequent |
| **Spaced practice** | Same; Cepeda et al. 2006 [background] | Bring old skills back on a schedule, even after mastery. A "level cleared" screen must not mean "never seen again" |
| **Interleaving** | Rohrer et al.: cluster-randomised trial, 54 seventh-grade maths classes, unannounced test one month later, **61% interleaved vs 38% blocked** (WWC: meets standards without reservations) [snippet] | Mix problem types in a session (dilution + mass concentration + density) so students must **choose the method**, which is exactly what they fail at on a test |
| **Worked examples and fading** | Sweller and colleagues: novices learn more from worked examples than from solving unaided; **expertise reversal**: as skill grows, the same guidance hurts, so fade it [snippet] | Novice: show a solved case and ask for the next step; then partial; then full problem. The adaptive logic must **reduce** help as mastery rises |
| **Mastery learning** | Khan Academy-style mastery trials: +0.12 to +0.22 SD over a year in a ~11,000-student RCT (grades 3-8); larger only where use was ~1 h/week and supervised. Source is Khan's own efficacy blog [snippet, vendor] | Mastery gating works when use is regular; usage dose matters more than the badge |
| **Cognitive load** | Sweller; Makransky et al. 2019 [snippet]: adding immersive VR to a lab simulation gave **more presence but less learning** and higher cognitive load in 52 students; a different 2019 study on lab-safety training found VR helped on **transfer** and enjoyment | VR must earn its place; keep the scene sparse; do not add decoration that is not needed to solve the task |

### 1.8 Evidence quality and honesty rules
1. Many positive game studies compare a game to **nothing** or to a poor control; ask "compared to what?".
2. Vendor-reported figures (Labster "101% increase", Prodigy white papers) are **marketing until independently replicated**. [snippet]
3. Engagement metrics (time on task, streak length, DAU) are **not** learning. Plan at least one learning metric (delayed retest).
4. This reference is a design aid, not a research review. Where the owner needs a claim in public (portfolio text), re-read the primary paper.

---

## 2. Teenagers (seconde) and the two subjects

### 2.1 Seconde students (about 15 years old)
Mostly [background] and [judgment]; the French school facts come from the project docs.
- **Social evaluation is intense.** Teens are highly sensitive to peer judgment. Public ranking and "kiddie" visuals are the two fastest ways to make a 15-year-old drop an app. Prefer a **clean, slightly "adult" aesthetic** (lab, workshop, detective, tech), private progress, humour that is not childish.
- **Autonomy matters more than at collège.** Choice of topic, a "skip diagnostic" option, adjustable difficulty, no forced daily ritual.
- **Utility value.** Teens engage when the practice visibly helps a test (contrôle/DS) or a real task. French seconde context: the official text asks for "automatismes" and personal work in and out of class [fact]; a ministry resource reportedly recommends 2-3 short questions in under 10 minutes [snippet in project doc]. So **short, frequent sessions that map to the programme** are the natural format.
- **Math/chemistry anxiety and identity.** A student who thinks "I am bad at maths" reads every red cross as proof. Feedback must keep failure about the **step**, not the person. Anonymity lowers anxiety in quiz games (Kahoot studies, small and self-reported) [snippet], while time pressure and fear of losing raise it.
- **Seconde is a transition.** Students arrive with very different collège levels. A short diagnostic and adaptive start is both a pedagogical and a motivational need (nobody wants to start with something far below or above them). [judgment; supported by the programme re-listing collège prerequisites, per `seconde-programme-and-exercises.md`]
- **Phones are the competitor.** At home the app competes with social media. Friction (long loading, login, slow web build) kills use more than any design flaw. [judgment]
- **Attention and session length.** Home sessions 5-15 minutes are realistic [judgment]. VR sessions should stay short and comfortable (see 2.4).
- **Consent and privacy.** Most seconde students are 15 or older, so many can consent alone under the CNIL view relayed in project docs; real use still needs GDPR work. Not legal advice. Never publicly rank minors, never store identifying data, no manipulative retention tricks (see ethics list, section 4.6).

### 2.2 Cognitive load at this level
- Seconde chemistry and maths mix **multi-step procedures, units, notation, and abstract ideas**; working memory fills fast. [background: cognitive load theory]
- Rules: one new idea per screen; show the data needed, remove what is not needed; split a multi-step problem into guided steps for novices and merge them as mastery rises; keep notation consistent with the French textbook conventions (Cm, g/L, mL, NA).
- Do not add a story, timer, animation **and** a new interface at once. Add one layer at a time.

### 2.3 How the two subjects differ in gamification fit
| Aspect | Mathematics (seconde) | Chemistry / physique-chimie (seconde) |
|---|---|---|
| Nature | Abstract, symbolic, **hierarchical** (calculus-style prerequisites stack: numbers, algebra, functions) [judgment] | **Three representation levels** (macroscopic observation, particle model, symbols/equations) and quantities with units [background: Johnstone's triangle] |
| Typical content (2019 seconde, from background; programme text not read this session) | Numerical and algebraic calculation, functions, geometry, statistics and probability, algorithmics/Python [background] | See `docs/chemistry/projects/solo-tutor/seconde-programme-and-exercises.md` for the verified chemistry map |
| Natural game fit | Puzzles and **rule-based manipulation** (DragonBox-style equation solving), pattern discovery, graph/function exploration, number-line games, optimisation challenges | **Simulations and builders** (assemble molecules, fill glassware, balance), "predict then reveal", investigation cases, unit/quantity tasks |
| Verifiability by code | Very high for numeric and symbolic answers (CAS or tolerance) | High for numbers, choices, balancing; low for written justification |
| Typical misconception style | Procedural slips (sign, parentheses, fractions, simplification); conceptual (variable as unknown vs variable; function as rule) [background; Bordeaux/Publimath snippets list simplification, sign, parentheses and conversion errors] | Conceptual and quantity confusion: mole vs mass vs number of entities; density vs mass concentration; dilution (concentration changes, amount conserved) [per project docs, snippets] |
| VR value | Low for most; some for geometry in 3D [judgment] | Medium for hand/eye technique (pipetting, glassware) and particle scale; low for pure calculation [judgment, project docs] |
| Main design risk | "Chocolate-covered broccoli": an arcade wrapped around a worksheet; speed-based rewards that punish careful thinking | Visual spectacle that hides the concept; teaching hazardous procedures; correctness errors by a non-chemist author |
| Evidence available | More: DragonBox (mixed), Khan mastery RCT, interleaving RCT | Thin: small, mostly uncontrolled stoichiometry-game studies; PhET design research; virtual labs about equal to hands-on for concepts, worse for physical technique (RSC 2013 per project docs) [snippet] |

### 2.4 Subject-specific rules
**Both subjects**
1. **Explain the why, not just the how.** Both subjects are plagued by "formula as recipe" learning. Ask the student to choose or justify a method, not only run it.
2. Include **plausibility checks** (is 5000 mL of acid reasonable?). This matches the programme's "Valider" competence [fact, per project doc].
3. Units are a first-class citizen: every numeric task carries a unit and the checker detects unit slips as a named error.
4. Authentic problem contexts beat abstract drills for transfer, but keep the story thin enough not to add reading load.

**Maths**
1. Fluency (automatismes) and understanding are separate goals: use fast retrieval games for the first, exploration or predict-and-check for the second.
2. Interleave problem types (the strongest maths-specific evidence in section 1.7).
3. Make the structure visible (balance model, graph, geometry), as DragonBox does, but plan the **transfer** back to standard notation; DragonBox evidence is mixed on that point [snippet].

**Chemistry**
1. Link the three levels explicitly: show the same event as observation, particle picture and equation, and ask the student to move between them.
2. **Predict, then reveal** (productive-failure style) for concepts such as dissolution, conservation of mass, dilution.
3. Keep hazardous procedures virtual and non-imitable: show equations and results, not quantities and steps. Safety rule carried from the project: **add acid to water, never the reverse.**
4. Say plainly what the app does not train (real hand technique, written scientific communication). Virtual labs help concepts and preparation, not skill with real equipment [snippet].

---

## 3. Survey of existing products and projects

Evidence quality is stated for every row. I did not review internal metrics; where a vendor makes a claim, it is marked as such. No product here was tested hands-on in this session.

| Product | What it is / what it gamifies | What works | What fails or is unproven | Lesson for solo-tutor |
|---|---|---|---|---|
| **Khan Academy** (maths mostly) | Mastery-based practice, skill levels, points/badges as a light layer | A year-long mastery implementation: +0.12 to +0.22 SD in an RCT of ~11,000 grades 3-8; larger (0.44-0.47) only with about 1 h/week supervised usage [snippet; Khan's blog] | Gains depend on **dose** and on classroom support; vendor-authored summary | Mastery gating + regular small practice beats flashy mechanics. Make 10-15 min a week of use the target, not marathon sessions |
| **DragonBox Algebra / 12+** | Game that teaches equation manipulation by moving cards, gradually revealing symbols | A 7th-grade RCT (about 1,850 students, AERA Open 2023) showed higher post-test scores than active control for DragonBox 12+ and From Here to There; a follow-up reported maintained **conceptual** gains. Small studies mixed [snippet] | Aleven and Long (CMU) argued the game gives too much scaffolding; a small Norwegian vocational study found no gain; procedural gains faded at post-test [snippet] | Visual rule-play can build concepts; plan **fading** of the scaffolds and an explicit bridge to real notation |
| **Prodigy Math** | RPG with math duels; ads and membership upsell | Very high engagement, wide classroom adoption [snippet] | Independent causal evidence is thin (company white papers are correlational/retrospective); 2021 FTC complaint by child-advocacy groups about manipulative design and unsupported efficacy claims; critics say little teaching occurs between battles [snippet; advocacy] | Do not make the math a toll gate for the game. Avoid pay or pressure loops (also an ethics rule for minors) |
| **Duolingo** (language, but the model for "Duolingo-style math") | Streaks, XP, leagues, hearts | Huge retention; company claims a league feature raised learning time 17% [unverified] | Commentators and one qualitative study describe "playing the game, not the language", XP farming, streak anxiety; no strong independent learning RCT surfaced [snippet] | Copy the **short daily loop and bite-size lessons**; do not copy hearts, loss messaging, or league ranking for teens |
| **Kahoot! / Quizizz** | Live quiz game with timer, points, podium | Review of 93 studies: generally positive for performance, class dynamics and attitudes; non-graded play lowered anxiety; anonymity helped [snippet] | Time pressure, fear of losing; competition sometimes pulled attention from deep learning; mostly small, self-reported studies [snippet] | Good for **low-stakes retrieval and class review**. Use untimed or soft-timed rounds; keep results private. Poor fit for multi-step reasoning |
| **PhET Interactive Simulations** (physics, chemistry, maths) | Free simulations designed from 200+ student interviews: exploration, simple controls, real-world links | Strong design principles, huge reach (250M+ runs, all subjects, per project doc); design for engaged exploration and implicit scaffolding [snippet; fact in project doc] | Not a progression system; needs teacher guidance; chemistry-specific outcome data not found | Study its design principles: **minimal UI, direct manipulation, immediate visible consequence**, no unnecessary reward layer |
| **Labster** (virtual labs, mostly biology/chemistry at university) | Gamified virtual lab simulations with quizzes | Makransky 2016: equal wet-lab skill vs demonstration, higher self-efficacy and intrinsic motivation; 2024 biology RCT: **no learning difference vs conventional teaching** [snippet] | Vendor percentages (101%, 76%) are marketing claims; chemistry evidence = vendor case study without control [snippet] | Honest pitch: **motivation and preparation, not proven superior learning**. Same stance as the concept note ("no proof VR teaches better") |
| **VR labs generally** | Immersive lab simulations | Enjoyment, presence, sometimes transfer of safety training [snippet] | Makransky 2019: more presence, **less learning** and more cognitive load in a lab simulation; DCU review: cost, training, few long-term studies (project doc) | Keep VR scenes minimal and purposeful; compare with the PC version (the project already plans this) |
| **Chemistry and stoichiometry games** (small studies, various countries) | Board-like games, card games, video games | Reports of positive acceptance and some gains in pre/post designs [snippet] | No large randomised study or meta-analysis surfaced for stoichiometry or balancing; mostly uncontrolled | White space: a well-checked balancing/limiting-reagent game is plausible, but claim little and measure |
| **Cognitive-tutor style systems** (e.g. adaptive maths tutors) [background, not researched this session] | Step-by-step tutoring with hints and mastery tracking | Long research record in maths (Carnegie Learning lineage) | Not researched here | Solo-tutor's error-tag + mastery design belongs to this family; look up the literature before claiming novelty |

### 3.1 Cross-cutting lessons (judgment, supported by the table)
1. **Engagement is cheap, learning is costly.** The most gamified products have the weakest independent learning evidence.
2. **Mastery and feedback loops beat reward layers** (Khan, DragonBox conceptual gains).
3. **Usage dose matters**: a good product used 5 minutes a month does nothing; schedule matters (spacing).
4. **Competition is a double-edged tool**: good for some, harmful for weak or anxious learners; keep it optional, private or team-based.
5. **Teacher/class integration multiplies effect** (Khan supervised use, Wouters: combined with other instruction).
6. **Vendor evidence is marketing**; prefer your own small retest.
7. **A free, simple tool can beat a complex one** (PhET): do not use technology for its own sake.

---

## 4. Applying this to the solo-tutor project

### 4.1 What the project docs say (so this section stays grounded)
Read on 2026-10-15: `docs/chemistry/projects/solo-tutor/concept.md`, `seconde-programme-and-exercises.md`, `target-level-analysis.md`; `docs/architecture/architecture-overview.md`. Key facts:
- **Product**: solo seconde **chemistry** practice, same exercises on **PC (WebGL, home)** and **VR (Meta Quest, school)**, AI tutor that picks and explains, cloud pseudonymous profile, no chat storage, test data only. Pillars VR, gamification and AI weighted equally. [concept, decisions]
- **Brick = exercise family**: seeded parameters, **code-computed answer**, wrong-rule recomputation with **error tags**, fact sheet, difficulty, review status. Demo cap: 4 families (dilution, balancing + limiting reagent, mole by weighing, particle zoom diagnostic). [architecture section 6]
- **Code decides what to practise** (`TutorPolicy`); AI only composes variants and explains from the fact sheet; seeded fallback always exists. [ADR-003 in architecture overview]
- `Progression` (XP, level, streak) and mastery are **pure functions over the attempt list**; `Attempt` records `hintsUsed`, `durationMs`. [architecture section 6]
- AI usage has a **daily credit quota** per account. [ADR-007, Q7]
- Open design questions already listed: **Q8 (gamification frame that survives beyond one session)**, Q1 (audience), Q2 (teacher review).
- Concept's own risk: **"Seconde can feel like a worksheet; gamification is the weakest pillar at this level."**
- Unknown (not in the docs): the game fiction, the visual style, the reward rules, the session length, the competence metric, a school/teacher integration, any maths content, any measurement of learning.

### 4.2 What the project already does right (keep)
| Existing choice | Why it fits the evidence |
|---|---|
| Code-checked answers + wrong-rule error tags | Enables specific, informational feedback (1.6) and diagnosis of misconceptions (2.3) |
| Student production of answers (numbers, builds) | Retrieval practice (1.7) |
| Derived mastery/progression from attempts | Transparent, recomputable; supports spaced scheduling and honest progress display |
| 3e diagnostic bridge | Right start-of-year placement; avoids the "too easy / too hard" mismatch (1.5, 2.1) |
| "What does VR add over PC?" rule | Aligned with Makransky-type warnings (1.7, section 3) |
| No chat storage, pseudonym, test data only, no public data | Ethics baseline (1.4, 2.1) |
| Honest pitch ("no proof VR teaches better") | Aligned with Labster and VR evidence |
| Short-task, automatismes fit; teacher summary later | Matches the official recommendation of short regular practice |

### 4.3 Design rules for solo-tutor (do / don't)
Each rule names the learning goal it serves. They are guidelines for the GDD and feature specs, not decisions.

**A. Core loop and session**
| # | Rule | Learning goal | Risk if ignored |
|---|---|---|---|
| A1 | Home loop = **one session of 5-10 min: 3-5 tasks, always ending with a clear "done" state** (no infinite feed). Target aligns with "questions flash" format | Spaced, retrieval-based habit | Marathon sessions; compulsion pattern |
| A2 | Mix **2-3 skills per session** (interleave) instead of 10 dilution tasks in a row once the student has basic mastery | Choose-the-method skill | Illusion of mastery in blocked practice |
| A3 | **Resurface mastered skills** at growing intervals (spaced review) as quiet "refreshers", not as "you lost progress" | Retention | Level-cleared = forgotten |
| A4 | Adaptive difficulty target: students succeed most of the time with a stretch; **reduce hints as mastery rises** (fading) | Flow, expertise reversal | Boredom or anxiety; over-scaffolding |
| A5 | New concept (mole, dilution) first as **predict or attempt, then reveal**, then a worked example, then practice | Productive failure / concept | Recipe learning of formulas |
| A6 | Offer a **skip-diagnostic / choose-topic** path, with the tutor's suggestion visible | Autonomy | Forced path feels like homework |

**B. Feedback and error handling**
| # | Rule | Learning goal | Risk |
|---|---|---|---|
| B1 | On a wrong answer show the **error tag in plain French/English** ("you used the flask volume instead of the volume to take") and the **step** to redo; never only "wrong" | Corrective, informative feedback | Feedback that lowers performance |
| B2 | Retry the **same misconception with a new seed** soon after (and again later) | Fix the rule, not the number | Memorising an answer |
| B3 | **Never reward a wrong rule** (already in the exercise reference). A correct final number from a wrong method gets partial credit and a note | Method over luck | Rote use of formulas |
| B4 | Score the **4-step answer layout** (quantity, formula with units, operation, boxed result) as separate points, as the exercise reference suggests | Method, communication | Final-number-only habits |
| B5 | Hints: free, graded, and the first one always available; hint use lowers a bonus, never blocks progress, never shown to others | Help-seeking without shame | Hint avoidance or hint spam |
| B6 | Explanations from the fact sheet cite their fact; if the AI cannot, say "ask your teacher" (already in concept) | Trust, correctness | Wrong chemistry |
| B7 | Detect **gaming** (very fast random answers, repeating hints) from `durationMs` and `hintsUsed` and respond gently (suggest slowing down, switch to a worked example), not with penalties | Learning, not score farming | XP farming |

**C. Rewards and progression**
| # | Rule | Learning goal | Risk |
|---|---|---|---|
| C1 | **Mastery map** per skill (particles, atoms, formulas, mole, balancing, limiting reagent, dilution) is the primary progress display; XP and level are secondary | Competence | Points becoming the goal |
| C2 | XP only for **new correct method use, correct recovery after an error, spaced review success**; capped per day; easy repeated items give little | Quality over quantity | Farming |
| C3 | **Streak**, if any, is weekly and forgiving (for example "3 sessions this week"), no loss messages, no content locked behind it | Spacing without anxiety | Streak anxiety, compulsive use |
| C4 | **No lives/hearts, no timers that cost points, no pay-to-progress** | No punishment for mistakes | Dark patterns, anxiety |
| C5 | **No leaderboards among students.** Allowed: personal bests, "beat your last order", team goals if a teacher enables them later | Competence and relatedness | Social comparison harm |
| C6 | Badges: few, **informational** ("first correct dilution without help"), not tied to quantity of play | Competence evidence | Overjustification |
| C7 | Any cosmetic reward (bench decoration, lab coat) is **unexpected or tied to mastery**, never promised for "just doing more" | Intrinsic motivation | Overjustification |
| C8 | AI-credit quota is **invisible to the student when possible** (silent fallback to seeded exercises), and never shown as a countdown or scarcity currency | Fairness, no pressure | Artificial scarcity loops |

**D. Fiction and style**
| # | Rule | Learning goal | Risk |
|---|---|---|---|
| D1 | The **fiction is the task** (client order, quality control, case file, production line). It should explain **why** the numbers matter. Fiction is a documented moderator of behavioural effects (Sailer and Homner) | Meaning, transfer | Decoration only |
| D2 | One fiction per skill cluster is enough: technician fiction for dilution/calibration/identification; **puzzle** frame for Lewis, ions, balancing (the exercise reference already says technician fiction does not fit Lewis) | Fit | Forced story |
| D3 | Visual style: clean, slightly "adult" (lab/workshop/tech), schematic over photoreal (Clark 2016 snippet; Quest performance) | Low cognitive load, teen acceptance | Childish look, high art cost |
| D4 | Humour and tone: neutral, friendly tutor; no sarcasm, no "oops you failed" | Safe failure | Anxiety |
| D5 | Keep a hard separation between **game state** ("order failed, client unhappy") and **chemistry truth** ("this rule is wrong"). The story can fail; the student never feels punished | Safe failure | Confusing the two |

**E. VR versus PC (platform-specific)**
| # | Rule | Reason |
|---|---|---|
| E1 | Same checker, same seeds, same error tags on both (already in the architecture); **progression and rewards are identical** across platforms | Fairness; cross-device continuity |
| E2 | VR only where the body or scale matters (dilution bench: choose glassware, pipette, fill to mark; particle zoom). PC is the full-feature path | VR value test; Makransky cognitive-load warning |
| E3 | VR session budget: short (about 10-15 min), seated or standing at a bench, no artificial locomotion (already in the architecture), comfort breaks (judgment) | Comfort; cybersickness risk |
| E4 | VR UI: few, large, world-space panels at arm's length; calculations done on a **simple pad or PC-like form**, not by typing in the air | Ergonomics, accuracy |
| E5 | In VR, hands-on technique can add **physical stakes** (wrong glassware shows an error margin), but the learning point must still be explicit in feedback | Link action to concept |
| E6 | State on the PC build when a brick is not available in VR and vice versa; no platform feels second-class | Equal weight decision |

**F. AI tutor**
| # | Rule | Reason |
|---|---|---|
| F1 | AI explanations use the same error-tag vocabulary as the checker; the student sees a **short explanation first, with "more" on demand** | Cognitive load; autonomy |
| F2 | AI never judges correctness; never reveals the answer before an attempt unless the student asks for a worked example | Retrieval practice |
| F3 | The AI adds visible value where rules cannot: **free-text "why" questions** and **contextual error explanations**. Make that visible in demo, as the concept already asks | Justifies the pillar |
| F4 | Warn the student not to type personal data; cap length (already in architecture) | Privacy |
| F5 | Persona neutral, not "pretend human friend" that builds dependency (minors) | Ethics |

### 4.4 Candidate gamification frames for Q8 (options, with a recommendation)
Q8 asks for a frame that survives beyond one session. Options (judgment):
| Option | Idea | Fit with rules | Risk |
|---|---|---|---|
| **1. Lab-technician career** (recommended) | You run a small testing lab: client orders (dilution, identification, calibration) arrive; each skill cluster unlocks a "department"; progress = **competence rating per department** (mastery map), optional cosmetic upgrades unlocked by mastery | Meaningful fiction (D1), mastery map (C1), no lives, fits dilution/calibration/identification and the VR bench | Reward economy tempts coins; keep it to mastery-based unlocks |
| 2. Case-file detective | Weekly cases that chain several bricks (identify the unknown, check a label) | Interleaving built in; story variety | Content cost per case; weak fit for mole/balancing |
| 3. Production line / factory | Reactor chef: balance and run a line; limiting reagent stops the line | Strong for balancing and stoichiometry; natural visualisation | "Optimise for score" can reward speed over reasoning |
| 4. Pure mastery map, no fiction | XP-free progress, only skill levels | Least risk, cheapest | The "worksheet" risk named in the concept |

Recommendation: **Option 1 as the umbrella, with Option 3 as one department**, because it uses the documented technician fiction and the existing four families, and keeps rewards tied to mastery. This is a recommendation, not a decision; the owner decides.

### 4.5 Measuring whether it works (missing today)
The architecture records attempts but defines no learning measure. Proposed minimum (design level, no estimates):
1. A **diagnostic** (exists) used again as a **delayed re-check** (for example after 2-4 weeks) with new seeds, so improvement is measured on unseen items.
2. Per-skill **error-tag trend**: a tag that stops recurring is the best evidence of real learning.
3. **Transfer items** in a different surface form (same dilution idea in a new fiction).
4. Separate **engagement metrics** (sessions per week) from **learning metrics**; report both honestly in the portfolio.
5. With test data only, state that the demo measures **plausibility**, not effect. A real effect claim needs real students and a teacher.

### 4.6 Ethics and safety (for minors)
- No public ranking; no social comparison; no streak loss messaging; no lives; no countdown scarcity; no variable-reward loot boxes; no notifications designed to pull students back (if notifications ever exist, opt-in, scheduled, non-guilt).
- No punishing mistakes: errors lead to a hint or an explanation, not loss of progress.
- Privacy as in the project: pseudonym, summary-only storage, no chats stored, delete/export. Real use needs GDPR and EU AI Act review (not legal advice; see concept section 9).
- Chemistry safety: hazardous procedures stay virtual, no copyable quantities and steps; visible rule "acid into water, never the reverse".
- Accessibility (spec-level): colour-blind-safe codes (never red/green alone), readable text sizes, captions for any audio, alternatives to precise motion in VR (snap or assisted placement), a non-VR path for every brick.

### 4.7 Checklist (use when writing or reviewing any brick or feature)
**Before building a brick**
- [ ] Which programme skill (and which collège prerequisite) does it train? Named in the data.
- [ ] Which misconception or error tags does it detect? Reviewed by a teacher?
- [ ] Does the student **produce** an answer (not just pick)?
- [ ] Is there a worked example and a fade path for novices?
- [ ] Does it have a **VR-vs-PC** statement ("VR adds ...", or "PC only, because ...")?
- [ ] Is the fiction the task, and thin enough not to add reading load?

**Before shipping a session design**
- [ ] 5-10 minute sessions with a clear end?
- [ ] Interleaving and spaced review in the scheduler?
- [ ] Hints graded and never blocking?
- [ ] Feedback names the error and the next step?
- [ ] Rewards informational, capped, mastery-based?
- [ ] No leaderboards, lives, loss streaks, timers that cost, or artificial scarcity?
- [ ] No cheap way to farm XP?
- [ ] Mistakes cost nothing but a hint?
- [ ] Same progression and rewards on VR and PC?
- [ ] Safety and privacy rules respected?

**Do / don't summary**
| Do | Don't |
|---|---|
| Mastery map, informational badges | Public leaderboards, badge collecting as goal |
| Retrieval, spacing, interleaving, fading | Blocked drills, endless same-type practice |
| Explain the error with a tag | "Wrong" only |
| Fiction as the task | Quiz with a skin |
| Short, finishable sessions | Infinite feed, forced daily streak |
| Autonomy: choices, skip, opt-out | Forced path, forced badges |
| Be honest about what VR and AI add | Claim better learning without evidence |
| Measure learning separately from engagement | Treat time-on-task as success |

### 4.8 Design implications to take to the GDD (next step: `gdd.md`)
1. Define the **core loop** at two timescales: the 30-second task loop (see problem, act, check, error tag, retry) and the 5-10 minute session loop (3-5 mixed tasks, end screen with mastery change).
2. Specify `TutorPolicy` behaviour as **learning rules**: interleave, space, fade hints, repeat misconception with new seed. (Specification of behaviour only; architecture is the tech-architect's job.)
3. Specify `Progression` rules (what earns XP, caps, level meaning, streak form) with the ethics constraints in 4.6; flag to the tech-architect that `Progression` currently has "XP, level, streak" without rules.
4. Pick the **Q8 frame**, then write feature specs per brick with a VR flow and a PC flow.
5. Specify the end-of-session and "welcome back" screens (empty, error, success states).
6. Add a measurement feature (diagnostic re-check, error-tag trend) to the feature list.

### 4.9 Conflicts and doubts to flag (do not resolve here)
- **Architecture vs ethics rule:** `Progression` includes a **streak** by name; this reference recommends a forgiving weekly form or none. Needs an owner decision (and an update to the architecture only through tech-architect).
- **Quota vs flow:** the daily AI credit limit could appear as a hard stop mid-session. Needs a seamless fallback (already planned in ADR-007 per overview) and a rule that the student never sees "no AI left" as a penalty.
- **Scope:** three equal pillars plus two platforms is a documented solo-dev risk; the architecture's M1-M4 web-first cut line is consistent with this reference (the learning loop must work without VR).
- **Maths:** the project has no maths content. If the owner wants maths, it is a new scope item for the project-manager and tech-architect (new families, a symbolic checker). Not assumed here.
- **Off-programme content:** mol/L and molar mass are première, per the exercise reference; keep them out unless a teacher says otherwise.

### 4.10 Open questions (with my recommendation)
| # | Question | Recommendation |
|---|---|---|
| 1 | Is maths in scope at all? | No for the demo; keep chemistry. Use this reference's maths parts only if a later project starts |
| 2 | Real audience (Q1): portfolio, teachers, students? | Decide before the GDD; it changes whether teacher-facing mastery data comes before cosmetics |
| 3 | Will anyone check bricks (Q2)? | Strongly yes; a wrong rule teaches wrong chemistry |
| 4 | Streak or no streak? | Weekly goal, forgiving, or none |
| 5 | Who tests the app with a real seconde student (even 2-3 volunteers, with consent)? | Do it once the web product exists; watch for boredom and confusion, not just scores |
| 6 | Do cosmetic rewards exist? | Optional, mastery-linked, small; skip for the demo |
| 7 | Language of the UI: French, English or both? | Not documented; students are French; decide early because the content, tags and fact sheet depend on it |
| 8 | Is "AI tutor" visible as a character? | Neutral helper, not a person-like friend (minors) |

---

## Sources
Verified by search summaries in this session (accessed 2026-10-15) unless noted. Summaries only, not full papers; re-read primary sources before quoting numbers publicly.
- Sailer and Homner 2020, The gamification of learning: a meta-analysis, Educational Psychology Review 32(1). https://link.springer.com/article/10.1007/s10648-019-09498-w ; https://opus.bibliothek.uni-augsburg.de/opus4/frontdoor/index/index/docId/109056
- Other gamification meta-analyses (summary list): https://www.ncbi.nlm.nih.gov/pmc/articles/PMC10591086/ ; https://www.frontiersin.org/articles/10.3389/fpsyg.2023.1253549/full
- Wouters et al. 2013, serious games meta-analysis, J. Educational Psychology. https://www.e-teaching.org/materialien/literatur/wouters-van-nimwegen-van-ooostendorp-van-der-spek-2013
- Clark, Tanner-Smith, Killingsworth 2016, Digital Games, Design, and Learning, Review of Educational Research 86(1). https://www.sri.com/publication/education-learning-pubs/digital-learning-pubs/digital-games-design-and-learning-a-systematic-review-and-meta-analysis-brief/
- Deci, Koestner, Ryan 1999, Psychological Bulletin 125. https://depts.washington.edu/techdocs/papers/deciExtrinsicRewardsAndIntrinsicMotivation99.pdf ; dispute: https://pmc.ncbi.nlm.nih.gov/articles/PMC2731358/
- Mekler et al. 2017, Computers in Human Behavior 71. https://edoc.unibas.ch/32047/
- Hanus and Fox 2015, Computers and Education 80 (secondary summaries). https://www.smhp.psych.ucla.edu/pdfdocs/gamil.pdf ; https://flipeducation.ai/teaching-wiki/gamification
- Dunlosky et al. 2013, Psychological Science in the Public Interest (press summary). https://www.psychologicalscience.org/news/releases/which-study-strategies-make-the-grade.html ; DOI 10.1177/1529100612453266
- Rohrer et al., interleaved maths practice RCT (IES/WWC). https://ies.ed.gov/ncee/wwc/Study/88770 ; https://ies.ed.gov/use-work/awards/systematic-replication-study-interleaved-mathematics-practice
- Expertise reversal and worked examples (overview). https://openlearning.mit.edu/mit-faculty/research-based-learning-findings/worked-and-faded-examples ; https://faculty.engineering.asu.edu/mre/wp-content/uploads/sites/31/2020/02/Exp_Rev_LI06.pdf
- Sinha and Kapur 2021, productive failure, Review of Educational Research (summaries only). https://research-collection.ethz.ch/handle/20.500.11850/572828?show=full ; DOI 10.3102/00346543211019105
- Kluger and DeNisi 1996 feedback meta-analysis and critique. https://pluto.huji.ac.il/%7Emskluger/files/Download/Kluger%20&%20%20DeNisi%20abstract.doc ; https://researchschool.org.uk/sandringham/news/effective-feedback-the-research-evidence
- DragonBox: https://doaj.org/article/28d05a10d8ea487f80d0c3b6811e3e9d (AERA Open 2023) ; https://www.cmu.edu/homepage/computing/2014/spring/fun-and-games.shtml ; https://mdsoar.org/handle/11603/19951
- Prodigy: https://edweek.org/technology/popular-interactive-math-game-prodigy-is-target-of-complaint-to-federal-trade-commission/2021/02 ; https://fairplayforkids.org/pf/prodigy/ ; vendor claims https://www.prodigygame.com/blog/prodigy-works ; trial registration https://clinicaltrials.gov/study/NCT03706144
- Duolingo: https://arxiv.org/pdf/2203.16175 ; https://www.pcworld.com/article/2924235/why-i-fell-out-of-love-with-duolingo.html ; https://desirabilitylab.com/backfill/backfill-2021-29-duolingo-streak-system
- Kahoot literature review (93 studies) and related: https://par.nsf.gov/servlets/purl/10284492 ; https://research.gold.ac.uk/id/eprint/39435/1/1-s2.0-S0360131520300208-main.pdf
- Khan Academy efficacy (vendor blog): https://blog.khanacademy.org/multiple-studies-show-khan-academy-drives-learning-gains-evidence-for-our-platforms-effectiveness ; https://ies.ed.gov/use-work/awards/khan-academy-resources-maximizing-mathematics-achievement-postsecondary-mathematics-efficacy-study?ID=1521
- Labster and VR: https://labster.com/guides/evidence-labster-virtual-labs-work (vendor) ; https://link.springer.com/10.1007/s10639-024-13261-2 (2024 RCT, biology) ; Makransky, Terkildsen, Mayer 2019 (Learning and Instruction) https://imotions.com/blog/adding-immersive-virtual-reality-to-a-science-lab-simulation-causes-more-presence-but-less-learning ; Makransky, Borre-Gude, Mayer 2019 https://test01.ku.dk/:obvius/pureproxy/3974268/en/publications/motivational-and-cognitive-benefits-of-training-in-immersive-virt
- PhET design research: https://phet.colorado.edu/publications/archive/PhET%20interview%20Paper%20Part%20I.htm ; https://experts.colorado.edu/display/pubid_35023
- Chemistry game studies (small): https://e-journal.undikma.ac.id/index.php/hydrogen/article/view/10192 ; https://irep.iium.edu.my/120122/ ; https://ve.scielo.org/pdf/ri/v39n84/art09.pdf
- French maths error resources (snippets): https://ent2d.ac-bordeaux.fr/disciplines/mathematiques/prendre-en-charge-lerreur-puis-la-remediation-et-lapprofondissement-a-laide-de-l-ia_traam-2025-2026/ ; https://eduscol.education.fr/document/22096/download ; https://bibnum.publimath.fr/AAA/AAA04036.pdf
- Project documents read: `docs/chemistry/projects/solo-tutor/concept.md`, `seconde-programme-and-exercises.md`, `target-level-analysis.md`; `docs/chemistry/notes/learning-and-practice-overview.md`; `docs/chemistry/README.md`; `docs/architecture/architecture-overview.md`.

Cited from background knowledge, **not** re-checked this session (verify before quoting): Ryan and Deci 2000 (SDT, American Psychologist, DOI 10.1037/0003-066X.55.1.68); Csikszentmihalyi (flow); Bjork and Bjork (desirable difficulties); Roediger and Karpicke 2006 (DOI 10.1111/j.1467-9280.2006.01693.x); Cepeda et al. 2006 (DOI 10.1037/0033-2909.132.3.354); Hattie and Timperley 2007; Johnstone (three levels of chemistry representation); Sweller (cognitive load theory); the seconde maths programme topic list; the 70-85% success target.

## What I did not verify
- Primary papers (only abstracts and secondary summaries read). Effect sizes may differ slightly by source (for example Kluger and DeNisi 0.38 vs 0.41).
- The current seconde maths programme text and French maths misconception data (DEPP) beyond three search snippets.
- Independent evidence for Duolingo's learning effect, and any large trial of chemistry balancing/stoichiometry games.
- Adolescent-specific motivation studies (teen statements rest on general literature and judgment).
- VR comfort limits for session length (judgment).

## Change log
- 2026-10-15: first version.

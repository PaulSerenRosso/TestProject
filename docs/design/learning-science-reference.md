# Learning science reference: principles for teachers and self-learners

Date: 2026-10-16. Status: Reference (durable, not a GDD). Owner: solo developer of the solo-tutor project.
Purpose: the main theories and good principles about how people learn, with evidence strength, how a teacher applies each, how a self-learner applies each, and which popular ideas to avoid. General (not game-specific, not subject-specific). The gamification layer lives in [`gamified-learning-reference-seconde.md`](gamified-learning-reference-seconde.md) and is not repeated here; this document is the "learning" layer under it.
Tags (same convention as the gamified reference): **[snippet]** = seen in a search summary this session, not read in full; **[background]** = well-known literature cited from memory, not re-checked this session; **[judgment]** = my opinion or inference. No source was read as a full paper, so nothing here is tagged "fact"; re-read primary sources before quoting numbers publicly.
Evidence strength scale used below: **Strong** = many controlled studies and/or meta-analyses, consistent; **Moderate** = good support but boundary conditions or mixed results; **Weak/contested** = small effects, replication or measurement problems; **Myth** = no support or refuted.

---

## 0. One-page summary

Top actionable principles, ranked by (evidence strength x ease of use):

1. **Retrieve, do not reread.** Trying to recall or solve from memory beats rereading, highlighting and summarising. Strong. [snippet: Dunlosky 2013 rated practice testing and distributed practice "high utility"; rereading, highlighting, summarising "low"]
2. **Space it out.** Several short sessions over days and weeks beat one long session. Strong. [snippet, background]
3. **Mix problem types (interleave) once the basics are there.** It makes practice feel harder and works better, especially in maths. Moderate to strong. [snippet]
4. **Give novices structure; remove it as they improve.** Worked examples, small steps, scaffolds, then fade. Unassisted discovery does worse than guided instruction. Strong. [snippet]
5. **Get specific feedback fast, on the task and the next step.** Quality matters more than quantity. Strong on average, but a minority of feedback hurts. [snippet]
6. **Build on what the learner already knows, and check for misconceptions.** Prior knowledge is the base of new learning, for good or bad. Strong. [background]
7. **Teach (or learn) the planning-monitoring-reflecting loop.** Metacognition and self-regulation have among the largest estimated gains per cost. Moderate to strong. [snippet]
8. **Keep working memory free.** One new idea at a time, remove irrelevant material, use pictures plus words where they carry different information. Strong (cognitive load theory), with many boundary conditions. [background/snippet]
9. **Motivation: competence, autonomy, relevance.** Progress people can see, real choice, a reason that matters. Moderate. Growth-mindset messaging alone is a weak lever. [background/snippet]
10. **Basics of the body.** Sleep, and focused attention without multitasking, support memory. Moderate. [snippet]

Biggest mistakes: believing "I understood it when I read it", cramming, matching teaching to "learning styles", praising effort as a substitute for teaching strategies, and measuring success by how fluent practice feels.

---

## 1. Ground rules for reading this document

1. **Effect sizes are not comparable across fields without care.** Hattie's "0.40 hinge point" and league tables of influences are criticised for mixing different designs, measures and contexts [snippet]. Use rankings as a hint, not a ranking.
2. **Lab results are often cleaner than classroom results.** Retrieval, spacing and interleaving come from controlled studies; classroom effects are usually smaller and depend on how well the technique is implemented. [judgment]
3. **"Works on average" does not mean "works for everyone"**. Prior knowledge changes what helps (see expertise reversal, section 5).
4. **Feeling of learning is a poor guide.** The techniques that work best (retrieval, spacing, interleaving) feel harder and less fluent. In one well-known experiment on interleaved study, about 80% of participants believed blocking worked better although interleaving gave better test results [snippet, secondary description of Kornell and Bjork 2008].
5. **Always ask "compared to what?"** and **"measured when?"** (immediately, or after a delay).

---

## 2. Memory-based principles (the strongest evidence)

### 2.1 Retrieval practice (the testing effect)
- **What it says:** Recalling information from memory strengthens it more than restudying it. The test is a learning event, not just a measurement. Roediger and Karpicke 2006 are the classic study. [background]
- **Evidence:** **Strong.** A meta-analysis of 61 studies (Rowland 2014) is reported with an effect of about 0.50 favouring testing over restudy [snippet, secondary review]. Dunlosky et al. 2013 gave practice testing the highest utility rating across ages and tests [snippet].
- **Boundary conditions:** Works best with feedback after the attempt (so errors do not get fixed in memory), and when the retrieval is effortful but successful. Low-stakes quizzing avoids anxiety. [background]
- **Teacher:** Start lessons with a few questions on earlier material; use short low-stakes quizzes, "brain dumps", exit tickets; require production (write, solve, explain), not recognition only; return corrected quizzes.
- **Self-learner:** Close the book and write what you remember; use flashcards in both directions; do past problems without notes first; check, then correct.
- **App link:** Players produce answers (type a number, build a molecule), not pick from lists (see gamified reference 1.7 and rule F2).

### 2.2 Spaced (distributed) practice
- **What it says:** The same amount of study spread over time gives better long-term retention than massed study ("cramming"). Cepeda et al. 2006 is the standard review. [background]
- **Evidence:** **Strong.** Rated high utility with practice testing [snippet]. Optimal gap depends on how long you need to remember: roughly, longer retention goals need longer gaps (Cepeda 2008, reported in a secondary review) [snippet; verify].
- **Practical numbers:** No universal schedule exists. A common rule of thumb is to review after a day, a few days, a week, a few weeks [judgment]. Do not over-engineer: any spacing beats none.
- **Teacher:** Build a spiral: revisit topics at growing gaps in homework, starters and tests; weekly and monthly reviews (this is one of Rosenshine's principles, section 7.1).
- **Self-learner:** Short daily sessions rather than one weekend block; schedule a review of each topic; spaced-repetition software (flashcard apps) automates it.
- **App link:** Mastered skills must resurface as quiet refreshers (gamified reference A3).

### 2.3 Interleaving
- **What it says:** Mixing different problem types or topics within a session (ABCABC), instead of blocking them (AAABBBCCC), improves the ability to choose the right method and improves delayed test results. [snippet]
- **Evidence:** **Moderate to strong, strongest in maths.** Brunmair and Richter 2019 meta-analysis (59 studies): overall g = 0.42, with the effect depending on similarity of the categories [snippet]. A cluster-randomised trial in 54 seventh-grade maths classes found 61% vs 38% on an unannounced test a month later [snippet, via the gamified reference].
- **Caveats:** Helps most when items are confusable and learners must discriminate; may not help for very different or very hard new material; novices need some blocked practice first. [judgment, background]
- **Teacher:** After introducing a method with a few blocked examples, mix old and new problem types in homework and quizzes.
- **Self-learner:** Shuffle your problem set instead of doing chapter-end exercises in order; at each problem, first name the method and why.

### 2.4 Desirable difficulties
- **What it says:** Conditions that slow learning now (spacing, interleaving, retrieval, generating answers) often improve retention and transfer later. Bjork and Bjork. [background]
- **Evidence:** **Umbrella concept built on 2.1 to 2.3**, each with its own evidence. Not every difficulty is desirable: if the learner lacks prerequisite knowledge, difficulty is only difficulty. [judgment]
- **Teacher:** Check that the difficulty is achievable with effort (see "high success rate", 7.1). **Self-learner:** Prefer the strategy that feels effortful but leaves you able to answer; do not judge by fluency.

### 2.5 Sleep and attention
- **Sleep:** Sleep after learning helps consolidate memories (Diekelmann and Born 2010 review) [snippet]. An experiment on adolescents with realistic shortened sleep (five nights at 6.5 h) found reduced learning, whereas many other findings are correlational [snippet]. Sleep-deprived people tended to rate their own performance more favourably than it was [snippet]. **Evidence: moderate.** Adolescents are the group where sleep loss is common. [snippet]
- **Attention and multitasking:** [background] Switching between tasks (phone notifications while studying) costs time and accuracy; no source checked this session, so treat as a general principle [judgment].
- **Teacher:** Do not schedule important new material late after sleep-deprivation periods; avoid all-nighter norms; give phone-free work blocks. **Self-learner:** Study, then sleep, then retrieve next day; put the phone out of reach for a focused block.

---

## 3. Cognitive load and instructional design

### 3.1 Cognitive load theory (Sweller)
- **What it says:** Working memory is small (handles a few new elements at a time) while long-term memory is large. Instruction should limit **extraneous load** (irrelevant demands), manage **intrinsic load** (complexity of the content) and promote **germane load** (effort on building schemas). [background]
- **Evidence:** **Strong as a design framework**; individual effects (worked examples, split attention, redundancy, expertise reversal) have many experiments; the three-type split is debated and revised in recent work [background; judgment].
- **Teacher:** Break problems into steps; put text and diagram where they can be read together (not on separate pages); remove decoration and redundant narration; introduce one new idea at a time.
- **Self-learner:** Study from a clean workspace and clear notes; work from examples first; if you are lost, shrink the step.

### 3.2 Worked examples and expertise reversal
- **What it says:** Novices learn more from studying solved examples (then partially solved, then full problems) than from solving unaided. As expertise grows, the same guidance becomes redundant and can hurt (**expertise reversal**, Kalyuga). [snippet: MIT teaching resource and Kalyuga paper, as listed in the gamified reference]
- **Evidence:** **Strong for novices**; the reversal effect is well replicated, so guidance must **fade**. [snippet]
- **Teacher:** Model every new procedure with a think-aloud, then give faded examples (blank out steps progressively), then independent practice. **Self-learner:** When starting a topic, read solved examples and explain each step to yourself; switch to solving first and checking after as you improve.

### 3.3 Multimedia and dual coding
- **What it says:** Dual coding (Paivio): information coded both verbally and visually can be remembered better. Mayer's multimedia learning principles: for example, words plus relevant pictures beat words alone; irrelevant material hurts. [background, snippet]
- **Evidence:** **Moderate.** A 2024 meta-analysis of Mayer's principle studies (92 articles, 591 effects) found g = 0.37 overall, with smaller or inconsistent effects for animations, games, simulations and no significant effect for VR in that analysis; independent work (Brom et al. 2018) found smaller effects for educational games than that analysis [snippet]. Principles are also criticised for narrow lab conditions [snippet].
- **Myth watch:** Dual coding is **not** "visual learners". It applies to everyone and to the content (a diagram of a process), not to preference. See section 9.
- **Teacher:** Use diagrams that carry real structure (timelines, particle pictures, graphs), explain them in words, and remove decorative images. **Self-learner:** Redraw a concept from memory, label it in your own words, and compare.
- **App link:** Chemistry's macro/particle/symbol links (gamified reference 2.4) are an application of this.

### 3.4 Guidance vs discovery
- **What it says:** Kirschner, Sweller and Clark 2006 argued that minimally guided instruction (pure discovery, problem-based, inquiry) is less effective and efficient for novices because it overloads working memory; the advantage of guidance recedes as prior knowledge grows. [snippet]
- **Evidence:** **Moderate to strong for the central claim.** A meta-analysis of 164 studies (Alfieri et al. 2011): unassisted discovery did worse than explicit instruction (d = -0.38), but **enhanced, guided discovery** did better than other instruction (d = 0.30); effective elements were feedback, worked examples, scaffolding and elicited explanations [snippet]. Critics note this shows the value of structure, not of discovery [snippet].
- **Reading:** The real choice is not "lecture vs inquiry"; it is **how much guidance, for whom, when**. [judgment]
- **Productive failure (Kapur):** Letting learners attempt a problem before instruction can improve conceptual understanding in some studies; evidence is mixed, with effect sizes not retrieved [snippet via the gamified reference 1.5]. Use for concept building, with explicit consolidation afterwards.

---

## 4. Feedback, assessment and mastery

### 4.1 Feedback
- **What it says:** Feedback should tell learners where they are, where they are going and what to do next (Hattie and Timperley 2007 framework; levels: task, process, self-regulation, not the person). [background]
- **Evidence:** **Strong on average, quality-dependent.** Kluger and DeNisi 1996: average effect about 0.4 but over a third of feedback interventions lowered performance; critics note most studies were not in schools [snippet via the gamified reference 1.6]. EEF Toolkit lists feedback as high-impact for low cost; figures vary by source (about +6 to +8 months) and I did not confirm the current number from the primary page [snippet, unverified].
- **Teacher:** Comment on the task and next step ("check your units in step 2"), not the person; give feedback while it can still be used (before the final test); allow resubmission; avoid marks without comments for formative work.
- **Self-learner:** Check answers against a model; write down why you were wrong; ask a teacher/peer for specific feedback on the process, not just "is this right".

### 4.2 Formative assessment
- **What it says:** Using evidence of learning during teaching to adjust teaching and learning (Black and Wiliam 1998). [snippet]
- **Evidence:** **Moderate.** The original claim of effect sizes 0.4 to 0.7 is famous, but it has been criticised for dated, untraceable and heterogeneous sources (Bennett 2011), and later estimates are lower (about 0.2 to 0.3, Kingston and Nash 2011) [snippet, secondary]. Still consistent with the general result that checking understanding often is useful. Rosenshine's "check for understanding" agrees (7.1).
- **Teacher:** Ask questions that reveal misconceptions (e.g., multiple-choice with plausible wrong answers); use mini-whiteboards so all students answer; adjust the next step to what you see. **Self-learner:** Do self-quizzes before the exam, not after; treat results as "what do I fix next".

### 4.3 Mastery learning and tutoring
- **What it says:** Bloom's mastery learning: break content into units, test frequently, give corrective feedback, and require mastery before moving on. Bloom's 1984 "2 sigma" claim says one-to-one tutoring plus mastery gave two standard deviations over conventional classes. [background, snippet]
- **Evidence:** **Mastery learning: moderate (positive, smaller than Bloom's headline).** The 2-sigma figure is questioned: it rested on two small dissertation studies (three weeks each) with narrow topic tests, and the tutoring group also had mastery-style testing and corrective feedback; later reviews found no tutoring study at 2 sigma (a review of 96 studies per von Hippel) and typical tutoring effects are lower (a pooled estimate around 0.37 SD; VanLehn 2011 reported 0.79 for human tutoring) [snippet, from Education Next and secondary sources]. Practical conclusion: **frequent testing with corrective feedback is a large part of the benefit**, and one-to-one tutoring is helpful but not magic. [snippet; judgment]
- **Teacher:** Define the unit goals, check each one, re-teach in a different way when many students miss it, and give extra practice rather than moving on. **Self-learner:** Do not move on from a topic until you can solve unseen problems from it; keep a "not yet" list.
- **App link:** A mastery map per skill follows this logic (gamified reference C1).

### 4.4 Bloom's taxonomy (what it is and is not)
- **What it says:** A classification of cognitive goals: remember, understand, apply, analyse, evaluate, create (revised version, Anderson and Krathwohl 2001). [background]
- **Evidence:** **A planning tool, not a theory of learning.** It is not an evidence-based claim that you must climb levels in order; people often need knowledge (recall) before higher-order tasks make sense. [judgment]
- **Teacher:** Use it to check that assessments are not only recall, while remembering that facts in long-term memory enable higher-order thinking. **Self-learner:** Ask "can I explain, use, compare?" not only "can I recite?".

---

## 5. Prior knowledge, schemas and transfer

### 5.1 Prior knowledge and schemas
- **What it says:** New learning attaches to existing knowledge structures (schemas). Prior knowledge can help or hinder; misconceptions persist if not addressed. It is the first principle in Ambrose et al., *How Learning Works* (2010). [snippet, background]
- **Evidence:** **Strong (core consensus in cognitive psychology and education research).** [background]
- **Teacher:** Diagnose before teaching (short pre-quiz, misconception questions); activate relevant knowledge; give explicit counter-examples to common misconceptions; teach vocabulary and prerequisite facts. **Self-learner:** Before a new chapter, write what you already know and what you predict; fill prerequisite gaps first (a hole in the foundations makes everything above harder).
- **App link:** The diagnostic bridge from collège to seconde is this principle.

### 5.2 Transfer
- **What it says:** Applying learning in new situations. **Near transfer** (similar problem) is common; **far transfer** (very different domain) is rare unless explicitly supported. Barnett and Ceci 2002 give a taxonomy of how far transfer goes. [snippet]
- **Evidence:** **Strong that far transfer is hard.** Sala and Gobet 2017 found weak evidence for far transfer from chess, music or working-memory training; a competing meta-analysis (Smithers et al. 2018) reported broader transfer, so it is contested [snippet].
- **Practical consequence:** Do not expect "brain training" or a single subject to improve general thinking; teach the target skills directly, with varied examples and contexts, and ask learners to compare cases to extract the underlying principle. [judgment]
- **Teacher:** Vary surface features (different stories, same structure); ask "what is the same here and there?"; assess on new contexts. **Self-learner:** After solving, restate the problem in a different context; teach it to someone.

### 5.3 Deliberate practice and expertise
- **What it says:** Expert performance is built by sustained, goal-directed practice slightly beyond current ability, with feedback and often a coach (Ericsson). [background]
- **Evidence:** **Moderate; effect size contested.** A meta-analysis of 88 studies (Macnamara et al. 2014) found practice time explained about 12% of performance differences overall (26% in games, 21% music, 18% sports, 4% education, under 1% professions); critics argue this understates well-designed deliberate practice because individualisation was ignored [snippet]. Reading: **quality of practice matters, hours alone do not**, and many other factors also contribute. [judgment]
- **Teacher:** Make practice specific (target a sub-skill), with immediate feedback and an achievable stretch. **Self-learner:** Pick the weakest sub-skill, practise it deliberately, record errors, ask for expert feedback.

---

## 6. Metacognition and self-regulated learning

- **What it says:** Metacognition = thinking about one's own thinking (knowing what you know, planning, monitoring, adjusting). Self-regulated learning (Zimmerman) is a cycle of **forethought** (goals, plan), **performance** (strategy use, self-monitoring) and **self-reflection** (evaluate, adapt). [snippet]
- **Evidence:** **Moderate to strong for practical interventions.** The EEF Toolkit lists metacognition and self-regulation among its highest-impact strands: about +7 months, revised down from +8 (effect size about 0.54, from 0.62; 20 studies in that update) [snippet]. EEF also notes that disadvantaged pupils may have fewer chances to develop these strategies unless taught explicitly [snippet]. Interventions work better when all three phases are included [snippet].
- **Calibration:** Learners are often overconfident. Teaching students about overconfidence plus retrieval practice improved calibration and first-exam performance in an intro biology course (n = 290 vs 251) [snippet]. Judging learning by familiarity ("I read it, it felt easy") is a trap. [snippet]
- **Teacher:** Teach strategies explicitly (how to plan, how to self-test), model your own thinking aloud, ask learners to predict their score then compare, use wrappers (before/after reflection on a task). **Self-learner:** Before: goal and plan; during: self-test, note confusion; after: what worked, what next. Predict your result before checking, then compare.

---

## 7. How to organise teaching

### 7.1 Rosenshine's Principles of Instruction
- **What it says:** Ten principles drawn from cognitive science, studies of master teachers and research on cognitive support (American Educator 2012): (1) begin with a short review of previous learning, (2) present new material in small steps, (3) ask many questions, (4) provide models, (5) guide student practice, (6) check for understanding, (7) obtain a high success rate, (8) provide scaffolds for difficult tasks, (9) require and monitor independent practice, (10) engage in weekly and monthly review. [snippet]
- **Evidence:** **Moderate; it is a synthesis**, not a single experiment. Its parts agree with retrieval, spacing, load and feedback. The "high success rate" number often quoted (about 80%) comes from process-product research on teachers [background]; treat it as a target, not a law.
- **Use:** A practical lesson skeleton for teachers; for self-learners, the same sequence works: review, small step, practise, check, independent practice, periodic review.

### 7.2 Constructivism vs direct instruction (reconciled)
- Constructivism = learners build knowledge actively on prior knowledge (Piaget, Vygotsky). This is a theory of **how learning happens**, not a prescription of "let them discover". Active **thinking** is needed; physical or open-ended activity is not necessarily active thinking. [background; judgment]
- Direct/explicit instruction with practice and feedback is well supported for novices (3.4, 7.1). Problem-based and inquiry methods work better with enough scaffolding or after a base of knowledge exists.
- **Rule of thumb:** explicit teaching first for new, complex material; more open problems as knowledge grows; always with feedback. [judgment]

### 7.3 Zone of proximal development and scaffolding
- **What it says:** Vygotsky: the zone between what a learner can do alone and what they can do with help. Wood, Bruner and Ross (1976) coined scaffolding: temporary support that is removed as skill grows. [background]
- **Evidence:** **Moderate; the ZPD is a useful idea, harder to test directly.** Scaffolding evidence is consistent with worked examples and guided discovery (3.2, 3.4). [judgment]
- **Teacher:** Give hints, partial solutions, sentence starters, then take them away. **Self-learner:** Use hints sparingly in order; try before looking; reduce the help each round.

### 7.4 Large-scale evidence syntheses (use with care)
- Hattie's Visible Learning and the EEF Teaching and Learning Toolkit rank influences by effect size or months of progress. Useful for finding promising ideas; criticised for mixing different studies, using an arbitrary 0.40 "hinge point", and treating effect sizes as universal (see section 1) [snippet]. Prefer the underlying studies and the conditions under which an effect holds.

---

## 8. Motivation

### 8.1 Self-determination theory (SDT)
- **What it says:** Motivation is sustained when three needs are met: competence, autonomy, relatedness; external motivation becomes durable when internalised (Ryan and Deci 2000). [background, snippet]
- **Evidence:** **Moderate to strong in education settings, mostly self-report.** [background]
- **Teacher:** Explain why content matters, give real choices (topic, order, format), give feedback that shows progress, avoid controlling language and public comparison. **Self-learner:** Pick goals that matter to you, track visible progress, find a study partner or community.
- **Link:** Detailed treatment of rewards (overjustification) is in the gamified reference 1.3 and 1.4.

### 8.2 Expectancy-value theory
- **What it says:** Effort depends on (a) the expectation of succeeding and (b) the value of the task (interest, usefulness, importance, cost) (Eccles and Wigfield). [background, not searched]
- **Evidence:** **Moderate; widely used, correlational and some intervention evidence.** [background]
- **Teacher:** Raise expectancy with achievable tasks and visible success; raise value by connecting to the learner's goals. **Self-learner:** Ask "how will I use this?" and start with a task you can win.

### 8.3 Growth mindset (with the caveats)
- **What it says:** The belief that ability can grow (Dweck) is linked to resilience and better outcomes. [background]
- **Evidence:** **Weak to contested for brief interventions.** A meta-analysis (Sisk et al. 2018; 273 studies on mindset-achievement, 43 on interventions) found weak overall effects, with some benefit for at-risk or low-SES students [snippet]. A national experiment (Yeager et al. 2019; about 12,500 ninth graders) found small improvement, about 0.10 GPA points in lower achievers, and effects depended on context such as peer norms [snippet]. Numbers from secondary write-ups; verify before citing.
- **Practical reading:** Praise **strategy, effort used well and progress**, not "you are smart"; but do not expect a poster or a one-hour lesson to change results. The conditions (support, norms, good teaching) matter more. [judgment]
- **Self-learner:** Treat mistakes as information; focus on strategies that you can change.

### 8.4 Self-efficacy and anxiety
- Believing "I can do this task" (self-efficacy, Bandura) predicts persistence; success experiences build it. Anxiety consumes working memory. [background, judgment] Low-stakes testing, safe failure and mastery-based progress serve both.

---

## 9. Myths and weak claims to avoid

| Claim | Verdict | Why / evidence |
|---|---|---|
| **Learning styles** (visual, auditory, kinaesthetic): teach to each person's style | **Not supported** | Pashler et al. 2008 reviewed the "meshing hypothesis": few rigorous studies met the criteria, and those found no support for improved learning from matched instruction. People do have preferences; matching teaching to them did not raise achievement [snippet] |
| **Learning pyramid** ("we remember 10% of what we read, 20% of what we hear ... 90% of what we do") | **Myth** | The percentages have no verifiable source; the original study appears lost; the order of potency is wrong. Often attributed to Edgar Dale's "cone of experience", which did not contain those numbers [snippet] |
| **We use only 10% of our brain** | **Myth** | About 47% of teachers in a UK/Dutch sample endorsed it (Dekker et al. 2012); an Italian survey of about 6,700 teachers found 46.7% [snippet] |
| **Left-brain / right-brain learners** | Myth [background] | Not searched this session; widely listed among neuromyths in the Dekker study family |
| **Rereading and highlighting are good study methods** | Low utility | Dunlosky 2013 rated them low; they feel productive because of fluency [snippet] |
| **Cramming works** | Works short term only | Spacing beats massing for retention (2.2) [snippet] |
| **Praise talent ("you're so smart") builds confidence** | Counterproductive risk | Linked to avoiding challenge in Dweck's work; evidence of mindset interventions is mixed (8.3) [background] |
| **Brain training games make you smarter in general** | Not supported | Far transfer is weak (5.2) [snippet] |
| **Hattie's 0.40 means "anything below doesn't work"** | Misuse | Criticised as arbitrary; Hattie himself rarely says to drop low-scoring influences [snippet] |
| **Bloom: 2-sigma tutoring effect is routine** | Overstated | Based on two small studies; later reviews find lower effects (4.3) [snippet] |
| **"Digital natives" multitask well** | Likely false [judgment] | Task switching costs apply to everyone; not searched this session |
| **Discovery learning is best because learners construct their own knowledge** | Overstated | Unassisted discovery underperforms; guided discovery works (3.4) [snippet] |

Note: the harm of believing neuromyths is itself debated (one group argues no evidence of effect on teaching practice) [snippet]. The recommendation is not to build a lesson on them, not to panic if you did.

---

## 10. Practical checklists

### 10.1 Teacher checklist (per unit or lesson)
- [ ] I know what students already know (quick pre-check) and which misconceptions are common.
- [ ] New content is chunked into small steps; each step is followed by student practice.
- [ ] I modelled the procedure (think-aloud) and gave worked examples before independent work.
- [ ] Support fades over time (partial examples, then full problems).
- [ ] Students retrieve from memory (questions, quizzes) at the start and during the lesson; everyone answers, not just volunteers.
- [ ] Practice is spaced: topics return after days and weeks, not only at the end of the unit.
- [ ] Practice mixes problem types once the basics are in place.
- [ ] I check understanding often and change what I do next based on the answers.
- [ ] Feedback is specific, about the task and the next step, and arrives while it can still be used.
- [ ] Success rate is high but not total; tasks are within reach with effort.
- [ ] Decorative or irrelevant material is removed; text and diagram are integrated.
- [ ] I teach strategies explicitly (how to self-test, plan, check), not just content.
- [ ] I explain why the topic matters and offer real choices where possible.
- [ ] Assessment includes new contexts (transfer), not only the exact practiced forms, and happens after a delay at least sometimes.
- [ ] No ranking in public; mistakes are safe to make.
- [ ] I am not basing choices on learning styles, the learning pyramid or similar myths.

### 10.2 Self-learner checklist (per topic or week)
- [ ] I started by writing what I already know and what I predict.
- [ ] I read worked examples and explained each step before solving alone.
- [ ] I close the book and recall; I do problems without notes first, then check.
- [ ] I scheduled reviews at growing gaps (next day, a few days, weekly), and I follow the schedule.
- [ ] I mix topics or problem types in practice sets and name the method before solving.
- [ ] I keep an error log (what went wrong, why, how to fix) and revisit it.
- [ ] I predict my score before checking and compare, to calibrate my confidence.
- [ ] I get external feedback regularly (teacher, answer key, peer, tutor), especially on method.
- [ ] I study in short, focused blocks without phone or multitasking; I sleep enough.
- [ ] I can explain the idea in my own words and apply it in a new context.
- [ ] I do not move on until I can solve unseen problems from the current topic.
- [ ] My goal is clear and meaningful to me, and I can see my progress.
- [ ] I avoid rereading and highlighting as my main strategy and ignore learning-style labels.

---

## 11. Connection to the project (brief)

Project context (from the gamified reference, which read the project docs on 2026-10-15): solo-tutor is a seconde chemistry practice app with PC and VR shells, code-checked answers, error tags and an AI tutor that composes and explains. This document adds the general theory beneath those design rules. [judgment]
- **Already aligned:** student produces answers (retrieval); error tags (specific feedback and misconception diagnosis); derived mastery (mastery learning); diagnostic bridge (prior knowledge).
- **Not specified yet, flagged in the gamified reference:** a scheduling rule that implements spacing and interleaving, hint fading (expertise reversal), a delayed re-check to measure learning (4.5 there). These are the learning mechanics most likely to determine whether the app works; they come from sections 2 and 3 here.
- **Metacognition feature idea (for the GDD, not decided):** ask the player to predict whether they will get the next task right, then show the result, to train calibration. Fits section 6.
- **Teacher-facing material:** sections 4, 7 and 10.1 could feed any teacher summary or guide; sections 2, 6 and 10.2 could feed a short "how to practise" onboarding for students. [judgment]
- Not a design decision: the owner and the game design flow decide what enters the GDD.

---

## Appendix A. Plain-language explainers

Short, concrete restatements of the concepts that are easiest to misread. [background; judgment]

### A.1 Interleaving (2.3)
- **Blocked:** 10 fraction problems, then 10 percentage problems. Inside a block you already know the method.
- **Interleaved:** fraction, percentage, ratio, fraction... You must first decide *which kind of problem it is*, then choose the method.
- It feels harder and practice scores are lower, but later test scores are higher because you learn to discriminate problem types, not only to run a procedure.

### A.2 Cognitive load (3.1)
- Working memory holds only a few new things at once. Three kinds of load: **intrinsic** (how complex the content is), **extraneous** (bad presentation, distractions: remove it), **germane** (effort that builds lasting knowledge: keep it).
- Practical rule for a beginner: small steps, no distractions, clear explanations.

### A.3 Worked examples and expertise reversal (3.2)
- A **worked example** is a problem already solved, with every step shown and explained. Example: "Solve 2x + 3 = 11. Subtract 3 from both sides: 2x = 8. Divide by 2: x = 4."
- Novices learn more from studying these than from struggling alone, because struggling without a method overloads working memory.
- **Expertise reversal:** once the learner knows the method, the same examples become redundant and slow them down; they should solve problems themselves. Guidance must therefore *fade* as skill grows.

### A.4 Guidance vs discovery (3.4)
- **Guidance** (explicit instruction): the teacher explains the concept, shows the method, then the learner practises.
- **Discovery:** the learner gets a problem or situation (for example a simulation) and works out the concept alone.
- Novices do better with strong guidance; pure discovery is slow and often leaves misconceptions. The best-supported middle is **guided discovery** (hints, feedback, scaffolds), or a short struggle followed by an explicit explanation (productive failure).

### A.5 Feedback (4.1)
- Weak: "Wrong, the answer is 12." Better: "You added instead of multiplying; check the units in step 2."
- Good feedback is about the task and the next step (not praise of the person), arrives while it can still be used, and asks the learner to act on it.

### A.6 Mastery learning and tutoring (4.3)
- **Usual school way:** time is fixed, results vary. The class moves on after two weeks whatever the scores, so a student with 50% on fractions arrives in decimals with a hole, and holes pile up.
- **Mastery way:** the result is fixed, time varies. Teach, run a short check, move on at about 80-90%; otherwise re-explain differently and practise the gap, then re-check. Most students can reach the goal given enough time and the right help. It matters most in cumulative subjects such as maths and chemistry.
- **Tutoring:** one teacher with one student sees exactly where the student is stuck and corrects at once.
- **Bloom's "2 sigma"** (tutored students beat about 98% of a normal class) is overstated; realistic tutoring gains are roughly 0.3 to 0.8 SD, still large. Do not promise "2 sigma".
- **For the app:** diagnostic, error tags, and blocking the next topic until the prerequisite is solid make the app a tutor most students could not otherwise afford.

### A.7 Transfer (5.2)
- Using what you learned in a new situation. Textbook problem solved, same problem in disguise failed = transfer failure. Helped by varied examples, interleaving, explaining the underlying principle, and practising in different contexts.

### A.8 Metacognition and learner choice: who decides the method?
Question raised for the app: should the learner pick how to learn (even if poorly), or should the system impose one way?
- **Evidence:** left to themselves, learners often pick comfortable but weak methods (rereading over self-testing) and, as beginners, judge their own needs poorly (calibration problem, section 6).
- **Forcing everything** also backfires: it undermines autonomy, a core SDT need (8.1).
- **Design answer (recommended middle path) [judgment]:**
  1. **The system owns the evidence-backed core**: retrieval, spacing, interleaving, feedback, mastery gating. Not optional.
  2. **The learner owns what the evidence does not decide**: topic order within the plan, context and theme, exercise format, pace, goals.
  3. **Explain why** ("this is harder now, you will remember more"), which gives a reason and keeps autonomy.
  4. **Teach metacognition**, for example predict-your-score before the result, and widen learner control as calibration improves.
- SDT autonomy means *endorsing* what you do, not unlimited choice; meaningful choices plus a rationale satisfy it.

### A.9 Self-determination theory vs Rosenshine
- **SDT (8.1):** motivation lasts when three needs are met: autonomy, competence, relatedness. Internal motivation lasts longer than pressure or rewards.
- **Rosenshine (7.1):** ten classroom rules: review, small steps, many questions, models, guided practice, check understanding, high success rate, scaffolds, independent practice, weekly and monthly review.

### A.10 Learning styles: myth, but state it precisely (section 9)
- **Myth:** the "meshing hypothesis": teaching a visual learner visually, an auditory learner aurally, a kinaesthetic learner with movement raises achievement. Pashler et al. 2008 found no good evidence; self-reported style also does not predict performance.
- **True:** people have preferences (affecting enjoyment and engagement); the best format depends on the **content** for everyone (geometry needs diagrams, pronunciation needs sound, a lab skill needs hands-on practice); combining formats helps everyone (dual coding); learners differ in **prior knowledge**, which really matters.
- **For the app:** no "learning style quiz" driving instruction. Adapt to level (diagnostic, mastery) and content type. Preferences may drive cosmetic and format choices only, never replace retrieval, spacing and feedback.

---

## 12. Sources

All accessed 2026-10-16 through search summaries only (no full papers read). Re-read primary sources before quoting numbers publicly.
- Dunlosky, Rawson, Marsh, Nathan, Willingham 2013, Psychological Science in the Public Interest 14(1), 4-58 (press summary). https://www.psychologicalscience.org/news/releases/which-study-strategies-make-the-grade.html ; DOI 10.1177/1529100612453266
- Pashler, McDaniel, Rohrer, Bjork 2008, Learning styles: concepts and evidence, Psychological Science in the Public Interest 9(3). https://digitalcommons.usf.edu/psy_facpub/1765/ ; https://fordhaminstitute.org/national/commentary/learning-styles-concepts-and-evidence
- Sisk et al. 2018, Psychological Science 29(4); Yeager et al. 2019, Nature 573 (secondary summaries). https://hhs.purdue.edu/skill-learning-and-performance-lab/wp-content/uploads/sites/43/2024/08/sisk-et-al-2018-to-what-extent-and-under-which-circumstances-are-growth-mind-sets-important-to-academic-achievement-two.pdf ; https://pubmed.ncbi.nlm.nih.gov/31494041/ ; https://www.edweek.org/leadership/national-study-bolsters-case-for-teaching-growth-mindset/2019/08
- Kirschner, Sweller, Clark 2006, Educational Psychologist 41, 75-86. https://research.ou.nl/en/publications/why-minimal-guidance-during-instruction-does-not-work-an-analysis/
- Alfieri, Brooks, Aldrich, Tenenbaum 2011, J. Educational Psychology 103(1). https://www.fisme.science.uu.nl/publicaties/literatuur/2011_alfieri_discovery_learning.pdf ; https://researchinnovation.kingston.ac.uk/en/publications/does-discovery-based-instruction-enhance-learning-a-meta-analysis-2/
- Rosenshine 2012, Principles of Instruction, American Educator 36(1). https://www.teachertoolkit.co.uk/2018/10/21/barack-rosenshine/ ; https://wegrowteachers.com/?p=30485 (secondary lists)
- EEF Teaching and Learning Toolkit (metacognition/self-regulation, feedback). https://educationendowmentfoundation.org.uk/news/latest-updates-to-the-toolkit/ ; https://educationendowmentfoundation.org.uk/news/how-do-we-teach-metacognition
- Macnamara, Hambrick, Oswald 2014, Psychological Science (press summary). https://www.psychologicalscience.org/news/releases/becoming-an-expert-takes-more-than-practice.html ; critique: https://link.springer.com/article/10.1007/s12144-021-02326-x
- Bloom's 2-sigma and critique: von Hippel 2024, Education Next. https://www.educationnext.org/wp-content/uploads/2024/03/ednext_XIV_2_von_hippel.pdf ; https://nintil.com/bloom-sigma/
- Black and Wiliam 1998, Inside the Black Box; critique summaries (Bennett 2011; Kingston and Nash 2011). https://www.michigan.gov/documents/mde/Inside_The_Black_Box_-_Black_and_William_601104_7.pdf ; https://hhk3.kau.se/onl181-blogposts/?p=764
- Hattie effect-size criticism. https://www.edweek.org/leadership/opinion-john-hattie-isnt-wrong-you-are-misusing-his-research/2018/06 ; https://ascd.org/el/articles/interpreting-education-research-and-effect-sizes
- Brunmair and Richter 2019, Psychological Bulletin (interleaving meta-analysis). https://www.psychologie.uni-wuerzburg.de/fileadmin/06020400/2019/Brunmair_Richter_in_press__2019_META-ANALYSIS_OF_INTERLEAVED_LEARNING.pdf ; Rowland 2014 testing effect (secondary): https://courseware.epfl.ch/assets/courseware/v1/fdde2f0aa590bf3b1324077a6bf1540c/asset-v1%3AEPFL%2BDEMO%2B2020%2Btype%40asset%2Bblock/Rowland2014-meta-analysis.pdf ; https://www.frontiersin.org/articles/10.3389/feduc.2021.581216/full
- Multimedia learning meta-analyses. https://par.nsf.gov/biblio/10637927 ; https://carlhendrick.substack.com/p/which-multimedia-strategies-actually ; https://ksvi.mff.cuni.cz/amulab/wp-content/uploads/2018/11/MultimLn3_BromHannemann_181117.pdf
- Dekker et al. 2012, neuromyths, Frontiers in Psychology. https://www.frontiersin.org/articles/10.3389/fpsyg.2012.00429/full ; learning pyramid: https://en.wikipedia.org/wiki/Learning_pyramid ; https://www.teachertoolkit.co.uk/2018/01/07/research-myth-1/
- Sleep: Diekelmann and Born 2010 (summary) https://research.uni-luebeck.de/en/publications/the-whats-and-whens-of-sleep-dependent-memory-consolidation/ ; adolescent sleep restriction study (summary) https://pmc.ncbi.nlm.nih.gov/articles/PMC6084755
- Self-regulation and calibration. https://link.springer.com/article/10.1007/s10648-022-09666-5 ; https://lifescied.org/doi/10.1187/cbe.18-10-0202 ; https://sites.lifesci.ucla.edu/psych-bjorklab/wp-content/uploads/sites/13/2016/11/YanBjorkBjork2016.pdf
- Transfer: Sala and Gobet 2017 (BPS summary). https://bps.org.uk/research-digest/no-far-transfer-chess-memory-training-and-music-just-make-you-better-chess-memory ; https://journals.sagepub.com/doi/10.1177/0963721417712760
- Ryan and Deci 2000, American Psychologist 55(1), 68-78. https://www.e-teaching.org/materialien/literatur/deci-ryan-2000
- Ambrose et al. 2010, How Learning Works. https://serc.carleton.edu/resources/42043.html
- Related project documents: [`gamified-learning-reference-seconde.md`](gamified-learning-reference-seconde.md) (gamification, teens, products, solo-tutor rules); `docs/chemistry/notes/learning-and-practice-overview.md`.

Cited from background knowledge, **not** re-checked this session (verify before quoting): Roediger and Karpicke 2006; Cepeda et al. 2006; Bjork and Bjork on desirable difficulties; Sweller on cognitive load; Paivio on dual coding; Kalyuga on expertise reversal (directly searched, no result); Hattie and Timperley 2007; Anderson and Krathwohl 2001; Vygotsky and Wood, Bruner and Ross 1976; Eccles and Wigfield expectancy-value; Dweck on mindset; Bandura on self-efficacy; Kapur on productive failure (via the gamified reference); the "about 80% success rate" figure.

## What I did not verify
- Any primary paper in full; effect sizes come from abstracts, press releases or secondary summaries and can differ across sources.
- Expectancy-value, Vygotsky/scaffolding, dual coding and Kalyuga: searched, but no supporting result returned; they rest on background knowledge.
- The "left brain/right brain" and "digital natives" claims and the multitasking cost.
- The current EEF figure for feedback (sources disagree).
- Adolescent-specific and French-curriculum applicability; the Rosenshine "80% success" number.

## Change log
- 2026-10-16: first version.

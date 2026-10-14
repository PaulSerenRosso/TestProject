# Brainstorm: AI-Assisted Teacher Lab Kit (Desktop Authoring + VR Runtime)

Date: 2026-10-13
Status: Core concept agreed. No research done yet. Experiment choice, transfer method and hand tracking are open.
Supersedes (as a fresh start): `docs/brainstorms/archive-2026-10-09/` (heat/air digital twin). Kept as archive; reuse only when the owner asks.

## 1. Summary
- Two small Unity apps linked by a data file. **Desktop authoring app**: a teacher chats with an AI, describes a practical chemistry experiment, and gets a structured experiment file (JSON) plus a readable summary. **VR runtime app** (Quest 2): a pre-built app that loads the file and builds the lab from a fixed catalog of objects. The teacher never opens Unity.
- The AI is truly needed: free-text request in, validated structured experiment out, with the ability to say "I can't do that, here is an alternative". Rule-based adaptive difficulty could not do this.
- The VR value argument is **"the mistake is the lesson"**: the student makes a dangerous or costly mistake safely and sees the consequence. It is not "cheaper than a real lab" and does not replace real training, only partially complements it.
- The teacher reviews and corrects the AI output (chat edits plus readable JSON/summary), which removes the risk of unchecked AI content on hazardous topics.
- Controllers first; hand tracking is an upgrade to test once the headset arrives.

## 2. Goal and context
- Owner: gameplay programmer building a portfolio in Unity (Unity 6.6, Quest 2 expected, not yet owned).
- Goal: show VR mastery through a few small exercises (controllers, grabbing, pouring, turning, snapping), show interest beyond video games (education, impact), and show AI used both in the build process (Claude Code agent pipeline) and in the product itself.
- Real AI, not faked, in the demo. Owner pays API costs during development and recording. The demo is a recorded video, not a public playable build.
- Scope must stay small and iterative.
- Previous direction (environmental digital twin) was set aside; the overall portfolio goal is unchanged.

## 3. Key questions
| Question | Answer |
|---|---|
| Why not one app with AI inside VR? | Voice input (speech-to-text) in VR is extra work, and typing in VR is poor. Splitting avoids it: AI conversation happens on desktop with a keyboard. |
| Is AI really necessary here? | Yes, if the input is free text and the output is a validated structured experiment. Must be obvious in the demo. |
| Is it cheaper than a real lab? | Weak argument (glassware is cheap, headsets cost per student). Not the pitch. The pitch is safe failure of dangerous/consumable steps. |
| What does VR teach? | Order of steps, setup and safety. Not manual dexterity (no real weight or haptics). |
| How do we avoid dangerous AI mistakes? | Fixed catalog of items; schema validation; teacher review and edit; AI may refuse or propose alternatives. |
| School or museum? | Same tools either way. Leaning school / higher-study framing, kept accessible. Museum is a possible extension. Open. |
| Which experiment? | Open. Needs "dangerous but you learn something cool". Distillation alone is not dangerous enough. Needs research with the owner's chemistry knowledge. |
| How does the file reach the headset? | Open. Candidates: USB copy, local network, cloud code. Needs research. |
| Preview on desktop? | No full simulation (out of scope). The readable summary plus JSON is the preview; testing is in VR. |
| Voice in VR? | Out of scope for the first version. |

## 4. Ideas and options

### 4.1 Architecture (proposed)
- **Experiment as data, not code.** The JSON lists catalog items, positions, a step graph, hints, and consequences of wrong actions.
- **Desktop authoring app** (Unity, UI Toolkit): chat with AI, summary panel, step list, export button. The AI is told the catalog and the schema; output is validated before export.
- **VR runtime** (Unity, Quest 2): reads the file, spawns items, runs steps, shows UI hints, plays consequences.
- **Pros:** teacher never touches Unity; safe, bounded AI; small scope; shows UI Toolkit, VR interaction and AI integration; clear demo story.
- **Cons:** catalog and schema design is real work; two builds to maintain; consequence animations (the "mistake is the lesson" moments) cost art/VFX time.

### 4.2 Transfer to headset (unverified, to research)
| Option | Pros | Cons |
|---|---|---|
| USB copy into headset storage | Simplest, no network | Android folder access limits may block the app from reading it; manual |
| Local network (desktop serves file, VR downloads) | No internet or cloud, more polished | Extra networking code |
| Cloud link or short code | Smooth for teachers | Hosting, cost, backend; leave for later |
Recommendation: start with USB, document the others as future work.

### 4.3 Input
- Controllers first for all interactions (grab, pick, pour, turn, snap, throw).
- Hand tracking as an upgrade after testing on the real Quest 2. Pouring, turning and snapping with bare hands are risky.

### 4.4 Audience framing
- School/higher-study: accessible, teacher is the user. Leaning this way.
- Museum: single headset, staff run experiments, visitors watch hazardous reactions. Same tools.

### 4.5 Experiment selection criteria (draft)
- A wrong order or wrong choice has a clear, visible consequence.
- The student learns something surprising and cool.
- Hazardous or consumable in real life, but appropriate for school level.
- Uses few interactions (fewer than four is fine).
- Avoid anything where the "wrong" steps work as instructions for harm.
- Example idea to evaluate with a teacher: diluting concentrated acid (add acid to water). Not yet validated.

## 5. Research
No research done in this brainstorm. Nothing below is verified.
- Everything in section 4.2 and the hand tracking claim is general knowledge and needs confirmation.
- The archived research (`archive-2026-10-09/`) covers a different topic. Its Unity/HTTP notes may be partly reusable.

## 6. Decision
Decided: two apps (authoring + VR runtime) linked by a data file; real AI (not faked); teacher-in-the-loop; controllers first; chemistry as domain; recorded demo.
Undecided: the specific experiment; school vs museum framing; transfer method; hand tracking scope; which AI provider.
Needed to decide: research items in the handoff, plus the owner's choice of experiment.

## 7. Handoff for project manager
Context: read sections 1 to 4 first. The owner is a gameplay programmer building a portfolio. Tools: Unity 6.6, Quest 2 arriving soon. Archive of the old project is in `docs/brainstorms/archive-2026-10-09/`.

Next steps:
1. **Research (brainstorm partner, research mode):**
   - How to transfer a JSON file to a Quest and read it in a Unity app (USB, local network, others), with Android storage limits.
   - Hand tracking in Unity 6 on Quest 2 (support, SDK, pouring/turning/snapping feasibility).
   - Existing VR chemistry labs and AI lab/scenario generators (prior art, gaps).
   - AI provider options for structured JSON output, schema validation and cost estimate for the demo.
   - Candidate experiments with a clear "mistake is the lesson", verified with sources and checked for safety/age level.
2. **Owner chooses** one first experiment (5 to 8 steps) and the school/museum framing.
3. **Define scope for the first release:** one experiment, catalog of about 6 to 10 items, three or four interactions, desktop chat plus summary, VR runtime with UI hints.
4. **Tech architect:** JSON schema, catalog definition, validation rules, how AI refusal/alternatives work, repo structure for two Unity apps (one project or two).
5. **Show the pipeline:** keep the visible AI-agent process (docs chain, decision log, rejected outputs) for the portfolio page.

Open risks:
- Hand tracking reliability (mitigated by controllers first).
- File transfer limits on Quest.
- AI output quality and hallucinated items (mitigated by catalog and validation).
- Scope creep: desktop simulation, voice in VR, cloud hosting, multiple experiments.
- Consequence visuals ("mistake" moments) may cost more than expected.
- Headset not yet owned, so on-device testing is delayed.
- Safety/credibility: content must be reviewed by a teacher or the owner's chemistry knowledge.

Open questions:
- Which experiment, and at what education level?
- School or museum framing?
- One Unity project with two build targets, or two projects?
- Should the portfolio page present the apps as one chain or as two?

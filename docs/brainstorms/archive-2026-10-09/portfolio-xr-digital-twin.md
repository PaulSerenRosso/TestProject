# Brainstorm: XR / Digital Twin Portfolio Project

Date: 2026-10-09
Status: Draft for review. Use-case choice still open, research needed.

## 1. Context and goal
- Owner: gameplay and UI developer, recently more on Unreal Engine than Unity.
- Goal: a portfolio project that proves skills in VR/XR, digital twins and visualization in Unity, and opens doors to environmental, green tech and social-impact work.
- Target audience is broad: impact studios, simulation, visualization and digital twin companies, and any game or scientific/application company. The message is: "this person has relevant prior experience and will adapt quickly."
- The project must also prove:
  - Current Unity mastery (Unity 6.6).
  - UI Toolkit and UI/UX design skills.
  - Gameplay-style interactivity.
  - Mastery of an AI agent pipeline (Claude Code agents), made visible.

## 2. Constraints
- Hardware: Meta Quest 2 (not yet owned, expected in a few weeks). Low-end hardware, so a stylized low-poly look.
- Engine: Unity 6.6.
- Timeline: something showable within one month, then monthly updates.
- Assets: a collection of free packs (characters, UI, sounds) in mixed styles. Pick one coherent style.
- Skills: no SQL or Python, and no backend needed.
- Existing material: an unfinished UI Toolkit project (JuiceGate inventories) that may be reused as the dashboard foundation. To be discussed later.

## 3. Decisions made
1. **Real vs. fake data is a false dilemma.** The project is based on real data. Architecture: a data-source interface (for example `IDataSource`) with three providers: simulated (development), live (HTTP/JSON via `UnityWebRequest`) and replay (recorded real data, for stable demos).
2. **No SQL, Python or custom backend.** Public APIs return JSON and Unity consumes them directly.
3. **Purpose: "help decide" with a light teaching layer.** The user pulls levers, sees consequences and compares scenarios. Scenario cards provide the teaching. Behavior change is out of scope.
4. **Interactivity must be real but scoped.** The key feature is **A/B scenario comparison** (side by side or ghost replay).
5. **Concrete, human-scale use case.** No generic "weather visualization". There is a real user, a real decision and agents at human scale (inspired by the hospital contagion example, scaled down).
6. **Desktop-first, VR in month 2.** Input-agnostic interaction logic, so VR is added once the headset arrives.
7. **Make the AI pipeline visible.** See section 6.

## 4. Candidate use cases (to be decided after research)
| Option | User | Decision | Notes |
|---|---|---|---|
| Classroom/office air quality (current favorite) | School or facility manager | Ventilation vs. energy cost | Simple well-mixed room model (CO2 per occupant), few agents, outdoor weather/air-quality data. Can grow: corridor, floor. |
| Heatwave in a care home/building | Facility manager | Shading, night ventilation, vulnerable occupants | Same structure, more climate-specific. |
| Flood/evacuation in a neighborhood | Planner | Evacuation and infrastructure | Strong visuals, much bigger scope. Later version. |
| Energy-decision twin (grid carbon intensity) | Building owner | When to run loads, solar/storage | Owner was not strongly attracted to it. |

Owner is not attached to a specific environmental theme. The topic must have a concrete use case and allow exploring scenarios at human scale.

Note: a full hospital contagion twin is too large for a first release. One room is the same idea at a fraction of the cost.

## 5. Open questions
- Which use case? (Research needed.)
- What can be reused from the UI Toolkit project? (Discussed later.)
- Does Unity 6.6 support world-space UI Toolkit well enough for VR panels? Verify in the docs. Fallback: UI Toolkit for desktop and screen-space, uGUI for VR panels.
- Which free APIs are reliable, keyless and permitted for portfolio use? Verify terms before relying on them (candidates: Open-Meteo, UK Carbon Intensity API).
- How faithful must the model be? Plan: a simplified model, clearly labeled as simplified in the UI.

## 6. AI pipeline as a visible skill
- Repo structure that shows the chain: `docs/brainstorms` -> `docs/project` -> `docs/architecture` -> specs -> commits.
- A short "How this was built" page with a diagram of the agent chain (brainstorm-partner, project-manager, tech-architect, unity-developer).
- Show control, not just output: review steps, tests, a decision log, and examples where agent output was rejected or fixed.
- Optional evidence: tasks per week, time saved.

## 7. Risks
- Scope creep (full building, many agents) kills the one-month release.
- Mixed asset styles look incoherent. Pick one.
- Quest 2 performance. Stylized, low-poly, early profiling.
- Real-data dependency (API downtime, rate limits). Replay provider mitigates it.
- Credibility of the model. Be honest about simplifications.

## 8. Proposed next steps
1. Research: simple room CO2/heat models, existing indoor-air and digital twin XR projects (benchmarks), open data APIs.
2. Choose the use case and write a one-paragraph vision.
3. Hand over to the project-manager agent: vision, MVP for month 1 (desktop, UI Toolkit dashboard, simulated provider, one decision loop plus A/B comparison), roadmap (month 2 VR plus first live data source, month 3 second scenario and polish).
4. Verify Unity 6.6 world-space UI Toolkit support.
5. Decide how to reuse the UI Toolkit project.

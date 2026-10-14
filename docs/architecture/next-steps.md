# Next Steps (architect handoff)

Written: 2026-10-14, end of the first architecture session. For the tech-architect agent starting with no chat memory, and for the owner.

## State at end of session
- Written in `docs/architecture/`: `architecture-overview.md`, ADR-001 to ADR-011, `server-api.md` (draft), `coding-standards.md`, `patterns.md`, `dev-workflow.md`.
- Not written yet: `tech-specs/` (no PM stories exist), any PM document.
- No Unity code, scene, package or setting was changed. Nothing is committed (`docs/architecture/` is untracked).
- Existing throw-away code: `TestUnityProject/Assets/Scripts/` (`CubeMover.cs`, `NewAssembly.asmdef`). To be removed in the first Core task.

## Owner actions (the architect cannot do these)
| # | Action | Why |
|---|---|---|
| 1 | Take 3 scope changes to the project-manager: PC preview in the authoring app, server (AI proxy, storage, memory), public repo including server code | Brainstorm said "no full desktop simulation"; PM docs do not exist yet |
| 2 | Schedule spikes SP-1 (Unity LTS check), SP-2 (build profiles), SP-3 (Newtonsoft) before M1 | Unverified assumptions in the overview |
| 3 | Choose the first experiment and education level (open question Q1) | Drives the brick list, rule families and SP-4 |
| 4 | Git automation setup: permission rules in `.claude/settings.json`, protect `main` on GitHub, add secret/local-config patterns to `.gitignore` (root and `TestUnityProject/`) | See `dev-workflow.md` section 3 |
| 5 | Create the private sibling folder `D:\Unity\TestProject-private` as its own git repo | ADR-006 |
| 6 | Decide license, reviewer for rule cards (Q4, Q5) | Before going public |

## Architect next session: order of work
1. **Read first:** `docs/project/` (vision-and-scope, roadmap, backlog, specs, change-log) once the PM has written them; then re-read this folder.
2. **Reconcile:** map provisional milestones M0-M5 in `architecture-overview.md` section 9 to PM IDs (E*, S*, T*). Update the overview where the PM scope differs.
3. **Absorb spike results** (SP-1 to SP-3; SP-4 after the experiment is chosen):
   - SP-1 outcome may change the Unity version and XR package versions in section 2.
   - SP-2 outcome decides Build Profiles vs Editor-script builds (ADR-001).
   - SP-3 outcome may change how `Core` references Newtonsoft (ADR-008).
   - Replace every `UNVERIFIED` that a spike settled, with source and date.
4. **Write tech-specs just in time** for the stories of M1 (and only M1), in `tech-specs/<ID>-<slug>.md`. Expected specs:
   - Project skeleton: folders, asmdefs, remove `Assets/Scripts/`, test assembly.
   - Core data model and JSON (experiment, catalog, `LabAction`, Author result), including the final schema.
   - Simulation core and the first rule family (+ cross-validation fixture if SP-4 allows).
   - Validator and headless Verifier.
   - Rule-card lookup and card data format.
   - Golden-experiment test harness and `MockAuthor`.
   - Pre-push hook script (tests + secret scan) and exact batch test flags.
   Each spec follows the format in the architect definition: link to PM spec, classes and responsibilities, data and events, files (verified vs to create), patterns used, risks, test approach, out of scope.
5. **Then M2 specs** (authoring UI screens, `ServerAuthor`, `IExperimentSource`), after M1 is done. Do not write M3-M5 specs yet.
6. **Update `server-api.md`** to final when the server story starts (language and host from SP-6).

## Decisions still open (do not decide silently)
| Id | Question |
|---|---|
| Q1 | First experiment and education level |
| Q2 | School vs museum framing |
| Q3 | Server language and host (SP-6) |
| Q4 | Rule-card reviewer |
| Q5 | Public repo license |
| SP-7 | Claude model, structured-output schema limits, cost per generation |

## Reminders for the next session
- Rules the architect follows: no edits outside `docs/architecture/`; PM backlog changes go through the owner; max 5 questions per turn, each with a recommendation; YAGNI challenge on every new abstraction.
- Hard cap from ADR-002: 2-3 rule families in the first release.
- The AI never writes rules, sources or review status (ADR-004).
- Headset expected about 2026-10-28 (owner statement); M5 is the first milestone that needs it.
- Worktree guard: this session wrote into the main checkout after the owner set `"worktree": {"bgIsolation": "none"}` in `.claude/settings.json`. Keep that in mind if the setting changes.

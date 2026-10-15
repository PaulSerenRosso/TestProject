# Next Steps (architect handoff)

Written: 2026-10-15, architecture session 2 (Lab Kit archived, Solo Tutor architecture written). For the tech-architect agent starting with no chat memory, and for the owner.

## State at end of session
- Active architecture: `architecture-overview.md`, `decisions/ADR-001..014`, `server-api.md` (draft), plus the shared `coding-standards.md`, `patterns.md`, `dev-workflow.md` (rewritten for Solo Tutor).
- Lab Kit is in `archive-2026-10-15-lab-kit/` (paused, not to implement).
- Not written yet: `tech-specs/` (no PM stories exist), any PM document.
- No Unity code, scene, package, setting or server code was changed. Existing throw-away code: `TestUnityProject/Assets/Scripts/` (`CubeMover.cs`, `NewAssembly.asmdef`), to be removed in the first Core task.
- Work is on branch `docs/architecture-solo-tutor`; commit status is in the git log.

## Owner actions (the architect cannot do these)
| # | Action | Why |
|---|---|---|
| 1 | Take the scope changes (overview section 13) to the project-manager | PM docs do not exist; Solo Tutor replaces Lab Kit and adds backend, WebGL, quota |
| 2 | Answer open questions Q1-Q10 (overview section 12), especially Q3 (project name/prefix), Q5 (pseudonym), Q6 (invite codes), Q9 (who picks the skill) | Names and auth choices are expensive to change later |
| 3 | Schedule spikes SP-1, SP-2, SP-3 before M1; SP-4 and SP-8 before M3 | Unverified assumptions in the overview |
| 4 | Update `.claude/agents/unity-developer.md` and any agent text that names Lab Kit files or `LabKit` namespaces (outside the architect's write scope) | The agent must read the new docs; also add `dotnet test` to its verify step once `server/` exists |
| 5 | Git automation: `.gitignore` additions (ADR-009), protect `main`, `tools/hooks/pre-push` (first Core/server task) | `dev-workflow.md` section 3 |
| 6 | Create the private sibling `D:\Unity\TestProject-private` as its own git repo | ADR-009 |
| 7 | Find a seconde teacher (or a teacher friend) to review bricks and facts (Q2) | Correctness trust (ADR-004, 014) |
| 8 | Decide license (Q10) and Quest hosting approach (Q4) | Before going public / before M6 |

## Architect next session: order of work
1. **Read first:** `docs/project/` once the PM has written it, then re-read this folder.
2. **Reconcile:** map provisional milestones M0-M7 (overview section 9) to PM IDs (E*, S*, T*). Update the overview where PM scope differs.
3. **Absorb spike results** and replace every `UNVERIFIED` that a spike settled, with source and date. SP-3 may change how `Core` is shared (ADR-005, 011); SP-4 may change the WebGL rules (ADR-008); SP-7 fixes model and schema limits (ADR-003, 007); SP-8 decides UI technology (ADR-013).
4. **Write tech-specs just in time**, M1 only, in `tech-specs/<ID>-<slug>.md`. Expected specs:
   - Project skeleton: folders, asmdefs, remove `Assets/Scripts/`, `server/` solution with `Tutor.Core.Shared` and `Tutor.Core.Tests`, path helper for fixtures.
   - Core content model and JSON (skills, bricks, facts, `ExerciseSpec`, final schema).
   - `Pcg32`, `SeededComposer` and the first family (dilution) with property tests and golden seeds.
   - `ExerciseSpecValidator` and `AnswerGuard`.
   - `TutorPolicy`, `MasteryCalculator`, `Progression`, `QuotaPolicy`.
   - Pre-push hook script (tests + secret scan) and exact batch test flags.
5. **Then M2 specs** (server skeleton: auth, DB schema, attempts, summary, quota, mock-AI) after M1 is done. Do not write M3+ specs yet.
6. **Update `server-api.md`** to final shapes as each endpoint's story starts.

## Decisions still open (do not decide silently)
| Id | Question |
|---|---|
| Q1 | Audience: portfolio only, or also teachers |
| Q2 | Teacher reviewer for bricks and facts |
| Q3 | Project name and code prefix (ASSUMPTION `Tutor`) |
| Q4 | Hosting so a headset can reach the server (SP-6) |
| Q5 | Pseudonym generated vs chosen (ASSUMPTION generated) |
| Q6 | Invite-gated registration (ASSUMPTION yes) |
| Q7 | Credit numbers (ASSUMPTION 20/day) |
| Q8 | Gamification frame |
| Q9 | Does the AI pick the next skill (ASSUMPTION no, code does) |
| Q10 | Public repo license |
| SP-7 | Claude model, structured-output limits, cost per exercise and answer |

## Reminders for the next session
- Rules the architect follows: no edits outside `docs/architecture/`; PM backlog changes go through the owner; max 5 questions per turn, each with a recommendation; YAGNI challenge on every new abstraction.
- Hard caps: 4 exercise families in the first release (ADR-002); 2 AI repairs per generation (ADR-003).
- The AI never writes answers, formulas, facts, sources or review status (ADR-003).
- Headset expected about 2026-10-28 (owner statement); M6 is the first milestone that needs it.
- Worktree guard: the owner set `"worktree": {"bgIsolation": "none"}` in `.claude/settings.json`; sessions write into the main checkout.

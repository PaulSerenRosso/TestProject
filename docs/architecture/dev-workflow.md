# Developer Workflow

Status: Active, updated 2026-10-15 for Solo Tutor (git section 3 unchanged). For the `unity-developer` agent and the owner. One task at a time.

## 1. Procedure per task

| Step | What | Gate |
|---|---|---|
| 1. Read | PM spec in `docs/project/specs/` (if present), the tech-spec in `docs/architecture/tech-specs/`, then `coding-standards.md`, `patterns.md`, relevant ADRs, then the real code, folders, asmdefs, `Packages/manifest.json` | Spec/architecture missing, thin or contradictory: list the gaps (max 5), hand back to the owner |
| 2. Plan | Files to create/modify, classes and responsibilities, Editor setup the owner must do, how each step is verified | Owner OK |
| 3. Implement | Smallest change that meets the acceptance criteria. Tests first or together for `Core` logic. Follow naming, patterns, asmdef layout. No refactors or features outside the spec | |
| 4. Verify | Recompile with no errors, Console clean, `run_tests` green, Editor wiring re-read, manual steps for what cannot be judged by CLI | Report what was and was not verified |
| 5. Report | Format below | |
| 6. Commit | Section 3 | |

## 2. Technical definition of done (on top of PM quality gates)
- Compiles; Console has 0 errors and no new warnings. Server code: `dotnet build` has 0 warnings-as-errors.
- New or changed `Core` behavior has tests; the whole Core suite is green in Unity and by `dotnet test` (once `server/` exists); server changes have API tests.
- No layer rule violated (asmdef references match `architecture-overview.md` section 5); no WebGL-forbidden API in shared assemblies (`coding-standards.md` section 8).
- Naming, templates and patterns follow the docs; no unused code; no commented-out code.
- No secrets, no absolute local paths, no `.env` content in the diff; no student text logged or stored (ADR-006).
- New JSON content validates and is covered by the content, golden-seed or property tests.
- WebGL-affecting changes: say whether a WebGL build was tested in a browser, or "not verified in a browser".
- Tech-spec checklist ticked; deviations reported (section 7).
- Not verified items listed honestly ("not verified on device").

## 3. Git, branches, commits, PRs
- Branch from `main`: `feature/<id>-<slug>` (for example `feature/S1.2-pour-rule`), or `docs/<slug>`, `fix/<id>-<slug>`, `spike/<id>`.
- Commit: Conventional Commits with the PM ID when one exists: `feat(S1.2): add mixing heat rule`, `test(S1.2): ...`, `docs: ...`, `chore: ...`. Small, one logical change each.
- **Never commit to `main` directly. Never force-push.** Push the feature branch and open a PR with `gh pr create` (title = commit style, body = report). The owner reviews and merges.
- Before each commit: `git status`, check the diff for secrets and generated junk; keep `.meta` files with their assets; never commit `Library/`, `Temp/`, `Logs/`, `UserSettings/`, build output.
- **Permission model (decided 2026-10-14, `.claude/settings.json`):** read-only git, `git add` and branch creation run freely. `git commit`, every `git push` and `gh pr create` are gated: the owner approves each in the permission prompt. Push to `main`/`master`, force flags, `reset --hard` and `git clean` are denied.
- Rules match the command text only and cannot see the current branch (variants such as `git push origin HEAD:main` are not caught). The real guard is GitHub branch protection. If a command is denied, the agent reports it and stops; no workaround.
- **Who uses git:** every agent (`unity-developer`, `project-manager`, `tech-architect`, `brainstorm-partner`) and the owner, under the same rules. Each agent commits only its own files, on a branch named for its work: code on `feature/` / `fix/` / `spike/`, documents on `docs/<slug>`. Commit prefix `docs:` for documents. The owner approves every commit, push and PR in the permission prompt, then reviews and merges on GitHub.

### Automation setup (owner actions, outside the architect's write scope)
| # | Action | Status |
|---|---|---|
| 1 | Permission rules in `.claude/settings.json`. Use single spaces in patterns; `Bash(git push *)` already covers all pushes. | Done, clean up spaces |
| 2 | Protect `main` on GitHub (require PR, no direct push) | To do |
| 3 | `.gitignore`: confirm `Library/ Temp/ Logs/ UserSettings/ Builds/`; add `.env*`, `*.local.json`, `secrets/`. Enable GitHub push protection when the repo goes public. | To do |
| 4 | `tools/hooks/pre-push` (first Core task): refuse `main`, secret scan; EditMode run added once Core tests exist | To do |
| 5 | Align agent definitions: `unity-developer` Git section follows this document; the other agents get the same shared Git block (below). Also update `unity-developer` for Solo Tutor: new doc paths, `Tutor.*` prefix, server work (`dotnet test`) | To do |

Shared Git block for every agent definition (replaces any "commit only on request" wording):
```
## Git
- Follow `docs/architecture/dev-workflow.md` section 3. Commit only your own files, on a branch (`docs/<slug>`, `feature/<id>-<slug>`, `fix/…`, `spike/…`). Never on `main`; never force-push.
- `git commit`, `git push` and `gh pr create` are gated: run them and the user approves in the prompt. Before committing, show `git status` and the diff summary. No secrets, no `Library/`, `Temp/`, `UserSettings/`, build output; keep `.meta` files.
- If a command is denied, report it and stop; no workaround.
```

## 4. Tests: how to run
- Editor: Unity CLI `run_tests` + `test_status` (see agent definition), or Window > General > Test Runner.
- Batch (hook/CI): `Unity -batchmode -projectPath <path> -runTests -testPlatform EditMode -testResults <file>`; exact flags to be confirmed against the Unity docs when the hook is written.
- Fast path (no Unity): `dotnet test server/Tutor.Core.Tests` runs the same Core tests; `dotnet test server/Tutor.Server.Tests` runs API tests. Both become available once SP-3 and the skeleton task are done (ADR-012).
- Run the server locally: `dotnet run --project server/Tutor.Server` with mock-AI mode on; the WebGL build is copied into `server/Tutor.Server/wwwroot/` by the build script.
- AI tests use recorded responses. No API key is needed to run any suite.

## 5. Where things go
| Output | Location |
|---|---|
| Code | `Assets/_Project/Scripts/<Layer>/` |
| Content (skills, bricks, facts) / presentation data | `Assets/_Project/Data/Content/`, `Assets/_Project/Data/Presentation/` |
| Core tests, fixtures | `Assets/_Project/Tests/...` (also compiled by `server/Tutor.Core.Tests`) |
| Server, server tests | `server/Tutor.Server/`, `server/Tutor.Server.Tests/` |
| Shared-Core project (links Unity sources, no copy) | `server/Tutor.Core.Shared/` |
| Builder scripts for bulk Editor work | `TestUnityProject/AgentScripts/` (outside `Assets/`) |

## 6. Report format
```
Task <ID> <title>: implemented | compiled, awaiting Editor confirmation
- Created/changed: <paths and one-line role>
- Editor wiring: <what was done through the CLI>
- Verification: compile OK, Console 0 errors, tests N/N green, wiring re-read
- Criteria: 1 pass, 2 pass ...
- Not verified: ...
- Deviations from docs: none | <list, see section 7>
- Ideas for PM: ...
- Proposed commit: feat(<ID>): ...
```

## 7. Flagging a deviation
If the docs force something wrong, or reality contradicts them:
1. Stop, do not work around it silently.
2. State in the report: document, rule, why it does not fit, proposed alternative.
3. The owner decides; technical changes go to the tech-architect (ADR or doc update), scope changes to the project-manager.
4. Until decided, do the smallest compliant thing or wait.
Developer agents never edit `docs/architecture/`.

## 8. Spikes
A spike (time-boxed experiment, 0.5-2 days) lives on `spike/<id>`. Its output is a short written result (what worked, numbers, decision) given to the architect; spike code is not merged unless a story adopts it.

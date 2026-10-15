# Architecture Overview: Solo Tutor (working title)

Status: Proposed, 2026-10-15. Written from the owner's decisions in the architecture session of 2026-10-15. Last update: 2026-10-15.
Readers: the owner (solo developer) and developer agents with no chat memory.

> **PM documents do not exist yet** (`docs/project/` is empty). Everything follows `docs/chemistry/projects/solo-tutor/concept.md` plus the owner's decisions below. Milestones M0-M7 are **provisional** and must be mapped to PM IDs (E*, S*, T*) once the project-manager writes them. Items marked `ASSUMPTION` or `UNVERIFIED` need confirmation. The previous architecture (Lab Kit) is archived in `archive-2026-10-15-lab-kit/`.

## 1. Context

| Item | Value |
|---|---|
| Product | One student app. The student practices **seconde chemistry exercises** (dilution, mole, balancing, limiting reagent, particle diagnostic), gamified, on **PC in a browser (WebGL)** or in **VR (Meta Quest)**. An AI tutor **generates exercise variants**, **answers questions** from a fixed fact sheet, and the app **adapts difficulty**. Exercises are not necessarily "experiments": any gamified practice task qualifies. |
| Core rule | **Code owns correctness.** The AI proposes parameters and wording; code computes every answer, validates every AI output, and falls back to code-generated exercises. |
| Accounts | Simple pseudonymous accounts + database + small backend (owner wants to show backend, auth and database skills). |
| Privacy | The server stores an exercise/profile **summary** under a pseudonym. No real personal data, no chat logs. Test data only (concept decision). |
| Goal | Portfolio piece: VR and web client, real AI integration with automatic validation, tested shared core, backend with auth and DB, readable public code. |
| Demo | Recorded video plus a WebGL build runnable on localhost. Real AI (Claude) in the final demo. |
| Owner | One gameplay programmer. Quest 2 headset expected about 2026-10-28 (owner statement, ASSUMPTION). |

### Scope warning (read this)
Accounts, database, quota, AI validation, WebGL, Quest, and three equally weighted pillars (VR, gamification, AI) is a large scope for one developer. Mitigation built into the plan: **M1-M4 is a complete product on the web** (no headset, no 3D). VR (M6) and the 3D lab (M5) come after. The cut line is documented in section 9. Each ADR below traces to a need; anything else is "not now".

## 2. What carried over from Lab Kit, and what changed

| Topic | Lab Kit | Solo Tutor |
|---|---|---|
| Apps | Authoring app (desktop) + Quest runtime | **One student app**, two shells: Web (WebGL) and Quest |
| Core model | Quantity simulation with rule families | **Exercise families**: seeded generation + code-computed answer + wrong-rule error tags (ADR-002) |
| AI role | Teacher chat, compose an experiment before publishing | **Run time**: compose exercise variants, answer questions, within a daily quota (ADR-003, 007) |
| AI guard | Verify-and-repair against a simulation | Validate-and-repair against exercise rules; code-generated fallback always available (ADR-003) |
| Reference engines | PHREEQC cross-validation (ADR-003 old) | Dropped: answers are arithmetic. Property tests + teacher review status (ADR-004) |
| Server | Thin pipe, no accounts, free language | **Real backend**: ASP.NET Core, accounts, DB, quota; shares `Core` source (ADR-005) |
| Privacy | Not an issue | Central: pseudonymous accounts, summary only (ADR-006) |
| PC target | Windows authoring app | **WebGL** served by the same server (ADR-008) |
| Unchanged | Plain-C# core, constructor injection, JSON + discriminator, public repo / private sibling, input abstraction, trust signals, test-heavy Core, no DI container |

## 3. Tech stack

| Item | Version / choice | Status |
|---|---|---|
| Unity | 6000.6.5f1 (`ProjectSettings/ProjectVersion.txt`) | Installed. Unity docs for 6000.6 are labeled "Alpha" (accessed 2026-10-15); Unity lists 6.3 LTS as latest LTS (search summary, official page not read). **SP-1.** |
| Render pipeline | URP 17.6.0 | Installed |
| Input | Input System 1.20.0 | Installed |
| Tests (Unity) | Test Framework 1.8.0 (NUnit) | Installed |
| UI | `com.unity.ugui` 2.6.0 and UI Toolkit module installed. World-space UI Toolkit for XR appeared in the 6.2 beta (Zenn article, accessed 2026-10-15); stable status not confirmed. **SP-8** decides one UI technology or two. | Installed / UNVERIFIED |
| Editor automation | `com.unity.pipeline` 0.8.0-exp.1 (Unity CLI used by the developer agent) | Installed |
| JSON | Newtonsoft (`com.unity.nuget.newtonsoft-json` in Unity; `Newtonsoft.Json` NuGet on the server) | **Not installed. Version UNVERIFIED. SP-3.** |
| WebGL | Unity WebGL build module | Not verified as installed in the Editor. **SP-4.** |
| XR | `com.unity.xr.openxr`, `com.unity.xr.interaction.toolkit`, `com.unity.xr.meta-openxr` | **Not installed. Versions UNVERIFIED (SP-1, SP-5).** OpenXR is the path (the Oculus package is deprecated from 6.5 per Unity docs, accessed 2026-10-14). |
| Server | **.NET 10 LTS** (support until 2028-11-14, Microsoft support policy snapshot dated 2026-09-08, accessed 2026-10-15), ASP.NET Core minimal APIs, EF Core + SQLite for dev/demo (Postgres later if hosted), JWT bearer tokens. SDK 10.0.203 installed on the owner's machine (`dotnet --list-sdks`, 2026-10-15). EF Core and package versions UNVERIFIED. | Decided (ADR-005), versions open |
| AI | Claude API, structured outputs (JSON schema), called **only by the server**. Candidate models for composing and explaining: a small fast one first; model, schema-subset limits and cost per exercise **UNVERIFIED: SP-7.** | Decided shape, details open |

## 4. Platform targets

| Target | Details |
|---|---|
| Web (PC at home) | Unity **WebGL**, desktop browsers (Chrome, Edge, Firefox; mobile browsers out of scope). Served as static files by the same ASP.NET Core server, so client and API share an origin (no CORS in production). Initial download size and load time budget: **ASSUMPTION, measure in SP-4.** Constraints in ADR-008: no managed threads, no `System.Net`, `UnityWebRequest` only. |
| Quest (VR at school) | Android ARM64 (IL2CPP), OpenXR, Meta Quest 2 first (3 and 3S same target). Controllers only. Hands deferred. The headset must reach the server over **HTTPS** (a `localhost` server is not reachable from a headset): hosting question Q4, spike SP-6. Quest 2 was discontinued in 2024; acceptable for a recorded demo. |
| Performance (Quest, ASSUMPTION, measure in SP-5) | 72 fps, mobile URP settings, minimal real-time lights, no heavy transparency, particles capped. Bench-scale scene. |
| Comfort | Standing or seated at a bench. No artificial locomotion, no forced camera movement. |
| Desktop fallback | The web build is the fallback for testing without a headset. XRI's simulator can be added later. |

## 5. Structure

### Repository (ADR-009)
```
D:\Unity\TestProject\               PUBLIC repo (git root)
  TestUnityProject\                 Unity project
  server\                           ASP.NET Core server + .NET test projects (public; no secrets)
    Tutor.Server\                   the web API
    Tutor.Server.Tests\             API + persistence tests
    Tutor.Core.Shared\              .csproj that COMPILES the Unity Core sources (linked files, no copy)
    Tutor.Core.Tests\               .csproj that runs the SAME NUnit Core tests with `dotnet test`
  docs\                             architecture/, project/ (PM), chemistry/, brainstorms/
D:\Unity\TestProject-private\       PRIVATE repo, SIBLING folder, never inside the public tree
```
**Source of truth for Core is the Unity folder.** The server project includes it with `<Compile Include="..\..\TestUnityProject\Assets\_Project\Scripts\Core\**\*.cs" />`, `LangVersion` pinned to the C# version Unity uses (Unity 6 uses C# 9 per my knowledge, UNVERIFIED: SP-3) and target `netstandard2.1`. Result: the server validates AI output with the exact code the client runs, and Core tests run in seconds without Unity (also solves CI licensing, ADR-012).

### Unity folders and assembly definitions (ADR-001)
An assembly definition (asmdef) makes a folder compile as its own module with explicit references, so the compiler enforces the layering.

```
Assets/_Project/
  Scripts/
    Core/        Tutor.Core     pure C# (netstandard2.1, no UnityEngine, no threads, no I/O)
      Content/     loaders and models for bricks, facts, skills (JSON)
      Exercises/   ExerciseFamily classes, ExerciseSpec, ExerciseInstance, CheckResult, ErrorTag
      Validation/  ExerciseSpecValidator, AnswerGuard (explanations)
      Learning/    TutorPolicy, MasteryCalculator, Progression, QuotaPolicy
      Random/      Pcg32 (own seeded generator)
      Json/        converters with "type" discriminator
    Net/         Tutor.Net      UnityWebRequest API client, token handling
    Lab/         Tutor.Lab      shared 3D presentation (bench, glassware, particles) for M5+
    Web/         Tutor.Web      WebGL shell: login, screens, mouse/keyboard input   (WebGL + Editor)
    Quest/       Tutor.Quest    XR shell: input, VR UI, pairing login               (Android + Editor)
    Editor/      Tutor.Editor   build scripts, editor tools                         (Editor only)
  Data/Content/                 bricks.json, facts.json, skills.json (ADR-011)
  Data/Presentation/            ScriptableObjects: content id -> prefab, color, icon
  Prefabs/  Scenes/  Materials/  Art/  UI/
  Tests/
    EditMode/Core/     Tutor.Core.Tests   (also compiled by server/Tutor.Core.Tests)
    Fixtures/Exercises/ golden seeds and worked examples with sources
    Fixtures/Ai/        recorded AI responses
    PlayMode/          Tutor.PlayMode.Tests (few smoke tests)
```
The existing `Assets/Scripts/` (`CubeMover.cs`, `NewAssembly.asmdef`) is a throw-away test: remove it in the first Core task. No shared `Ui` assembly yet: screens live in the shells until SP-8 shows one UI technology works on both (then extract a `Tutor.Ui`).

### Layers and allowed dependencies
| Assembly | May reference | Must NOT reference |
|---|---|---|
| `Tutor.Core` | nothing (Newtonsoft only) | UnityEngine, any other Tutor assembly |
| `Tutor.Net` | Core | Lab, Web, Quest |
| `Tutor.Lab` | Core | Net, Web, Quest, XR packages |
| `Tutor.Web` | Core, Net, Lab | Quest |
| `Tutor.Quest` | Core, Net, Lab, XR packages | Web |
| `Tutor.Editor` | any (Editor only) | referenced by none |
| `Tutor.Core.Tests` | Core | Net and above |
| `Tutor.Server` (not Unity) | `Tutor.Core.Shared` | any Unity assembly |

### Builds (ADR-001)
| Build | Platform | Scenes | Assemblies active |
|---|---|---|---|
| `Web-WebGL` | WebGL | `Web_Main` (+ `Lab_Bench` from M5) | Core, Net, Lab, Web |
| `Quest-Android` | Android | `Quest_Main` | Core, Net, Lab, Quest |

Selected by Unity Build Profiles (scene list per profile UNVERIFIED: SP-2). Fallback: two Editor menu items in `Tutor.Editor` calling `BuildPipeline`. Switching platform reimports assets: work on Windows/WebGL daily, switch to Android only for headset builds. The WebGL output is copied to `server/Tutor.Server/wwwroot/` by a script (task in M3).

## 6. Core model in one page

Plain C#, deterministic, no UnityEngine, no threads (ADR-002). It runs in tests, in the Web and Quest clients, and on the server.

| Concept | Meaning |
|---|---|
| Content | `skills.json` (skill graph: particles, atoms, formulas, mole, balancing, limiting reagent, dilution), `bricks.json` (per family: parameter ranges per difficulty, wrong-rule labels, fact ids, source, review status), `facts.json` (fact sheet: id, text, source, review status). Authored by the owner, reviewed by a teacher. **Never AI text** (ADR-003, 014). |
| `ExerciseFamily` | A C# class per exercise type (demo cap: **4 families**: dilution, balancing + limiting reagent, mole by weighing, particle zoom diagnostic). Builds an `ExerciseInstance` from a spec, computes the correct answer, and checks answers with **wrong-rule recomputation** (for example "forgot mL to L") returning an `ErrorTag`. |
| `ExerciseSpec` | JSON: `family`, `difficulty`, `skills`, `params` (numbers), `story` and `hints` (text **templates with placeholders**, for example `{targetMl}`), `factIds`. **No answer inside.** Produced by `SeededComposer` (code) or `AiComposer` (server). |
| `ExerciseInstance` | Spec + family = rendered statement (placeholders filled by code, so text cannot contradict numbers) + correct answer + wrong-rule answers. |
| `IExerciseComposer` | `SeededComposer` (Core, PRNG from a seed, always succeeds) and `AiComposer` (server, Claude structured output). Two real implementations (pattern 6). |
| `TutorPolicy` | Pure function: mastery summary + recent error tags -> next skill and difficulty. **Code decides what to practice; the AI only composes the exercise and explains.** (Owner may overrule: see ADR-003.) |
| `ExerciseSpecValidator` | Schema, family exists, params in range, answer computable and sane, difficulty inside the requested band, wrong-rule answers distinct, placeholders resolve, **no digits in free text outside placeholders**, skills and fact ids exist, safety word list. Returns all diagnostics. |
| `AnswerGuard` | For AI explanations: `status: answer | refused | out_of_scope`; `answer` requires at least one existing `factId`; length cap. Cannot prove the text is faithful to the facts: residual risk (section 8). |
| `Attempt` | `attemptId` (GUID), `exerciseId`, `answer`, `hintsUsed`, `durationMs`, `createdAt`. Append-only. |
| `MasteryCalculator`, `Progression` | **Pure functions over the attempt list**: mastery per skill, top error tags, XP, level, streak. Nothing is stored that cannot be recomputed ("derive, don't store"); the server caches the result as the profile summary. |
| `QuotaPolicy` | Pure rules: credit cost per action, daily limit, reset boundary. Enforced by the server (ADR-007). |
| `Pcg32` | Own seeded random generator. `System.Random` is not guaranteed identical across Mono, IL2CPP and .NET, which would break "same seed, same exercise on web, VR and server". Golden-seed fixtures detect drift. |

### ExerciseSpec (sketch; final schema in the Core tech-spec)
```json
{
  "schemaVersion": 1,
  "family": "dilution",
  "difficulty": 2,
  "skills": ["dilution", "mass-concentration"],
  "params": { "stockGPerL": 40, "targetGPerL": 10, "targetVolumeMl": 100 },
  "story": { "title": "Order {orderNo}", "text": "A client needs {targetVolumeMl} mL of solution at {targetGPerL} g/L from a stock at {stockGPerL} g/L. How much stock do you take?" },
  "hints": [ "Think about the dilution factor.", "The amount of solute stays the same." ],
  "factIds": ["f-dilution-conservation"]
}
```
Polymorphic `params` per family use an explicit `"family"` discriminator (ADR-011).

## 7. Data flow

```
Web or Quest client (Core inside)
  login ----------------------------> POST /auth/login ........ JWT (short-lived)
  next exercise --------------------> POST /exercises/next
        server: attempts -> Mastery (Core) -> TutorPolicy -> skill + difficulty
                QuotaPolicy ok?  -- no --> SeededComposer
                AiComposer (Claude, facts.json + bricks.json as vocabulary)
                  -> ExerciseSpecValidator (Core) -- fail --> repair (max 2) -- fail --> SeededComposer
                store spec in exercises bank, charge credit if AI was used
        <---------------------------- ExerciseSpec (no answer)
  client builds ExerciseInstance locally (Core), student answers, instant local check + feedback
  attempt --------------------------> POST /attempts (idempotent by attemptId)
        server re-checks with Core (own result wins), appends attempt, updates profile summary
        <---------------------------- result + summary (mastery, XP, streak, quota left)
  question -------------------------> POST /tutor/ask
        server: quota -> Claude (fact sheet + current exercise) -> AnswerGuard -> text + factIds
        question text is NOT stored, not logged
```
Development without the AI or network: server **mock-AI mode** returns recorded specs and answers; the client can run `SeededComposer` and local checks alone; the public repo runs fully offline this way.

## 8. Risks and time-boxed spikes

Hand to the owner to schedule with the project-manager (the architect does not edit the PM backlog).

| ID | Spike | Time | When | Question |
|---|---|---|---|---|
| SP-1 | Unity version | 0.5 d | Before M1 | Is 6000.6.5f1 stable enough or move to an LTS? WebGL, XRI and Meta OpenXR versions for it? |
| SP-2 | Build profiles | 0.5 d | Before M1 | Does a profile hold its scene list and defines (WebGL + Android)? Else Editor-script fallback. |
| SP-3 | Shared Core | 1 d | Before M1 | The Core asmdef compiles in Unity **and** via the linked-source `.csproj` (`netstandard2.1`, pinned `LangVersion`); Newtonsoft in both; a Core NUnit test runs in both `Test Runner` and `dotnet test` (fixtures path helper). |
| SP-4 | WebGL smoke | 1 d | Before M3 | WebGL build loads; login + fetch against ASP.NET Core on localhost; Brotli/gzip headers served correctly; Newtonsoft survives IL2CPP stripping (`link.xml`); load size and time measured. |
| SP-5 | Quest basics | 1-2 d | Headset arrives | HTTPS fetch on device, XRI version, 72 fps baseline, IL2CPP JSON. |
| SP-6 | Hosting | 1 d | Before M6 | Where the server runs so a headset reaches it over HTTPS (tunnel, small VPS, LAN with certificate); secrets handling; rate limiting. |
| SP-7 | AI schema and cost | 0.5-1 d | Before M4 | Which schema features structured outputs accept (unions/discriminators?), which model, cost per exercise and per answer, how many repairs happen in practice. |
| SP-8 | UI technology | 0.5 d | Before M3 | Does world-space UI Toolkit work with XRI on this Unity version? If yes, one screen set serves Web and Quest; if no, uGUI on Quest. |

Other risks:
| Risk | Mitigation |
|---|---|
| Wrong chemistry (the owner is not a chemist) | Every brick and fact has `source` and `reviewStatus`; teacher review (Q2); property tests (ADR-004); `Unreviewed` shown honestly |
| AI composes bad exercises | Validator + repair + seeded fallback (ADR-003); recorded real responses as fixtures |
| AI explanation drifts from the facts | Must cite existing fact ids; scoped prompt; refusal path; length cap. **Residual risk: Core cannot check that the prose is faithful.** Shown in the demo as "answers come from the fact sheet" |
| Cost / token abuse | Daily credits per account, global cap, invite-gated registration, request size caps (ADR-007) |
| Child typing personal data in free text | UI warning, 300-character cap, text never stored or logged; provider data-retention settings UNVERIFIED (SP-7) |
| Cross-device determinism | `Pcg32` + golden seeds (ADR-002) |
| WebGL limits | ADR-008 rules; SP-4 |
| Scope | Section 1 warning, cut line in section 9, 4-family cap |
| Public server abuse | ADR-005 and 007 controls; secrets policy ADR-009 |
| Real use with minors | Out of scope for the demo. GDPR/EU AI Act work needed before real use (concept note section 9). Not legal advice. |

## 9. Provisional milestones (to be mapped to PM IDs)

| # | Milestone | Headset | Cut line |
|---|---|---|---|
| M0 | Spikes SP-1 to SP-3 (SP-8 before M3) | No | |
| M1 | `Core`: PRNG, skills, content loaders, 2 families (dilution first), spec, validator, `SeededComposer`, mastery, progression, quota policy; tests also run by `dotnet test` | No | |
| M2 | Server skeleton: accounts + invite codes, DB, attempts, profile summary, quota table, mock-AI mode, API tests | No | |
| M3 | Web client (WebGL): login, exercise screen for calculation bricks, feedback, profile/progress; served by the server (SP-4) | No | |
| M4 | AI: `AiComposer` and `/tutor/ask` with validate-and-repair, recorded fixtures, real Claude (recommend pulling the first real-AI call into M2/M3 as soon as the schema is stable: prompt quality is the biggest unknown) | No | **End of the web product: the portfolio is already complete here** |
| M5 | `Lab` 3D bench + particle zoom, mouse/keyboard in the web build | No | |
| M6 | Quest app: XR grab, dilution bench hero brick, pairing-code login | **Yes** | |
| M7 | Teacher summary view (optional, deferred) | No | |

## 10. Key decisions

| ADR | Decision |
|---|---|
| [001](decisions/ADR-001-one-app-two-shells.md) | One Unity project, one app, two shells (WebGL, Quest), assembly-definition layering |
| [002](decisions/ADR-002-exercise-families-seeded.md) | Exercise families: seeded, code-computed answers, wrong-rule error tags (replaces the simulation) |
| [003](decisions/ADR-003-ai-composes-specs-validated.md) | AI composes specs and explanations; code validates; seeded fallback; code picks the skill |
| [004](decisions/ADR-004-correctness-evidence.md) | Correctness evidence: property tests, golden seeds, reviewed sources (no reference engine) |
| [005](decisions/ADR-005-aspnet-server-shared-core.md) | ASP.NET Core server with accounts and DB, compiling the shared Core |
| [006](decisions/ADR-006-privacy-by-design.md) | Pseudonymous accounts, summary-only storage, no chat storage, delete and export |
| [007](decisions/ADR-007-ai-quota-and-cost.md) | Daily AI credits per account, global cap, graceful fallback |
| [008](decisions/ADR-008-webgl-policy.md) | WebGL as the PC target and its coding constraints |
| [009](decisions/ADR-009-public-repo-private-deploy.md) | Public repo including server; private sibling; secrets policy (carried over) |
| [010](decisions/ADR-010-constructor-injection.md) | Constructor injection, no DI container (carried over) |
| [011](decisions/ADR-011-data-formats.md) | Newtonsoft with discriminator; content as JSON (carried over, adapted) |
| [012](decisions/ADR-012-test-strategy.md) | Test strategy: Core-heavy, runs in Unity and `dotnet test`, recorded AI (adapted) |
| [013](decisions/ADR-013-input-and-ui-across-platforms.md) | Same logic, per-shell input and UI; UI technology by spike |
| [014](decisions/ADR-014-trust-signals.md) | Source, review status and report link on bricks and facts (carried over) |

Other documents: [coding-standards](coding-standards.md), [patterns](patterns.md), [dev-workflow](dev-workflow.md), [server-api](server-api.md), [next-steps](next-steps.md).

## 11. Non-goals (for now)

- Teacher dashboard (M7, optional), classes and class codes, email, password recovery, social features.
- Offline queue for attempts (the attempt API is idempotent, so it is cheap to add later), native mobile apps, mobile browsers.
- AI-invented answer logic or new exercise families (families are code written by the owner).
- Voice, hand tracking, multiplayer, WebXR.
- A DI framework, event-bus frameworks, UniTask, ECS, vector memory, storing chat.
- Real minors' data; GDPR/AI Act compliance work (design shows the intent only).

## 12. Open questions

| # | Question | Answer by |
|---|---|---|
| Q1 | Real audience of the demo: portfolio viewers only, or also seconde teachers? | Owner |
| Q2 | Who reviews bricks and the fact sheet for correctness (seconde teacher)? | Owner |
| Q3 | Project name and code prefix. ASSUMPTION: `Tutor` (`Tutor.Core`, ...). Cheap to rename now, costly later. | Owner |
| Q4 | Hosting so a headset can reach the server over HTTPS (SP-6). | Owner + architect |
| Q5 | Pseudonym: **server-generated** (for example `brave-otter-42`, ASSUMPTION, best privacy, hard to type) or user-chosen with an "@ rejected / no real name" warning? | Owner |
| Q6 | Registration gating: **invite codes** (ASSUMPTION, protects the AI budget) or open? | Owner |
| Q7 | Daily credit numbers (ASSUMPTION: 20 per account, 1 per new AI exercise, 1 per regeneration, 1 per question; repairs free but capped at 2). | Owner |
| Q8 | Gamification frame that survives beyond one session (client orders, production line...). Architecture only provides `Progression`; design is a PM/brainstorm topic. | Owner / PM |
| Q9 | Should the AI also choose the next skill (ADR-003 says code does)? | Owner |
| Q10 | Public repo license. | Owner |

## 13. Scope changes to take to the project-manager

Registered by this architecture, not yet by the PM: (a) Solo Tutor replaces Lab Kit; (b) a backend with accounts, database and AI quota; (c) WebGL as the PC target served by the backend; (d) the Quest shell comes last, after a complete web product.

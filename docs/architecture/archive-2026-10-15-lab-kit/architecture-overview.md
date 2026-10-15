# Architecture Overview: Lab Kit (working title)

Status: Proposed, validated in discussion with the owner on 2026-10-14. Last update: 2026-10-14.
Readers: the owner (solo developer) and developer agents with no chat memory.

> **PM documents do not exist yet** (`docs/project/` is empty). Everything below follows `docs/brainstorms/vr-teacher-lab-kit.md` plus the owner's decisions in the architecture discussion. Milestones M0-M5 are **provisional** and must be mapped to PM IDs (E*, S*, T*) once the project-manager writes them. Items marked `ASSUMPTION` or `UNVERIFIED` need confirmation.

## 1. Context

| Item | Value |
|---|---|
| Product | Two apps linked by a JSON experiment file. **Authoring app** (Windows desktop): a teacher chats with an AI, reviews the experiment, previews it on PC, publishes it. **VR runtime** (Meta Quest): downloads the experiment by short code and plays it with controllers. |
| Core value | "The mistake is the lesson": the student makes a dangerous or costly mistake safely and sees the consequence. |
| Goal | Portfolio piece: VR interaction, UI Toolkit, real AI integration, tested architecture, readable public code. |
| Owner | One gameplay programmer. Quest 2 headset expected about 2026-10-28 (owner statement, ASSUMPTION). |
| Demo | Recorded video, not a public playable build. Real AI (Claude) in the final demo. |
| Chemistry | Domain only. The first experiment is **not chosen yet** (open question). |

## 2. Tech stack

| Item | Version / choice | Status |
|---|---|---|
| Unity | 6000.6.5f1 (`ProjectSettings/ProjectVersion.txt`) | Installed. Unity's 6000.6 docs are labeled "Alpha" (accessed 2026-10-14). **Check whether to move to an LTS release: SP-1.** |
| Render pipeline | URP 17.6.0 | Installed (`Packages/manifest.json`) |
| Input | Input System 1.20.0 | Installed |
| Tests | Test Framework 1.8.0 (NUnit) | Installed |
| UI, authoring app | UI Toolkit (module `com.unity.modules.uielements`) | Installed |
| UI, VR app | uGUI world-space canvas (`com.unity.ugui` 2.6.0). Chosen because it is the safe, documented path; world-space UI Toolkit not verified. | Installed |
| Editor automation | `com.unity.pipeline` 0.8.0-exp.1 (Unity CLI used by the developer agent) | Installed |
| JSON | `com.unity.nuget.newtonsoft-json` | **Not installed. Version UNVERIFIED. SP-3.** |
| XR | `com.unity.xr.openxr`, `com.unity.xr.interaction.toolkit` (XRI), `com.unity.xr.meta-openxr` | **Not installed. Versions UNVERIFIED.** Unity 6.6 docs list Meta OpenXR 2.6.0-pre.1 (a mirror lists 2.5.0-pre.1). The Oculus package is deprecated from 6.5, so OpenXR is the path. Source: https://docs.unity3d.com/6000.6/Documentation/Manual/com.unity.xr.meta-openxr.html (accessed 2026-10-14). |
| AI | Claude API with structured outputs (`output_config.format`, JSON schema). Source: https://platform.claude.com/docs/en/build-with-claude/structured-outputs (accessed 2026-10-14, search snippets only). Model choice and schema-subset limits **UNVERIFIED: SP-7.** | Called **only by the server** |
| Reference chemistry | PHREEQC (via Python) or published data tables, **offline only** | Feasibility for the first experiment UNVERIFIED: SP-4 |
| Server | Tiny HTTP service, language and host open (SP-6) | To decide |

## 3. Platform targets

| Target | Details |
|---|---|
| Authoring app | Windows x64 standalone. Keyboard and mouse. Contains the Lab preview. |
| VR runtime | Android ARM64 (IL2CPP), OpenXR, Meta Quest 2 first (3 and 3S use the same target). Controllers only. Hand tracking deferred (ADR-010). |
| Quest 2 status | Discontinued 2024; support end not officially announced, informal estimate about 2027 (TechRadar, accessed 2026-10-14). Acceptable for a recorded demo. Keep the build a generic OpenXR Android build. |
| Performance budget (ASSUMPTION, measure in SP-5) | 72 fps on Quest 2, mobile URP settings, minimal real-time lights, no heavy transparency, particles capped. A bench-scale scene (one table) keeps the load low. |
| Comfort | Standing or seated at a lab bench. **No artificial locomotion and no forced camera movement in v1.** Snap turn optional. |
| Desktop fallback | The keyboard preview is the fallback for testing without a headset (ADR-010). XRI's simulator can be added later for XR interaction tests. |

## 4. Structure

### Repositories (ADR-006)
```
D:\Unity\TestProject\               PUBLIC repo (git root)
  TestUnityProject\                 Unity project
  server\                           tiny server code (public; no secrets)
  tools\crossval\                   Python reference scripts (offline)
  docs\                             architecture/, project/ (PM), brainstorms/
D:\Unity\TestProject-private\       PRIVATE repo, SIBLING folder, never inside the public tree
                                    (deployment notes, hosting config; real secrets live in env / host secret store)
```

### Unity folders and assembly definitions (ADR-001)
An assembly definition (asmdef) is a Unity file that makes a folder compile as its own module; references between modules are explicit, so the compiler enforces the layering.

```
Assets/_Project/
  Scripts/
    Core/        LabKit.Core         pure C#, noEngineReferences = true
    Net/         LabKit.Net          UnityWebRequest clients (server author, experiment source)
    Lab/         LabKit.Lab          3D presentation shared by both builds (bench, containers, VFX)
    Authoring/   LabKit.Authoring    desktop UI, keyboard input, preview host   (Standalone + Editor)
    Quest/       LabKit.Quest        XR input, experiment loader, VR hints UI   (Android + Editor)
    Editor/      LabKit.Editor       build scripts, editor tools                (Editor only)
  Data/Catalog/                      substances, containers, tools, rules: JSON files (ADR-008)
  Data/Presentation/                 ScriptableObjects: catalog id -> prefab, color, VFX
  Prefabs/  Scenes/  Materials/  Art/  UI/
  Tests/
    EditMode/Core/   LabKit.Core.Tests
    Fixtures/CrossVal/    reference outputs written by tools/crossval scripts (ADR-003)
    Fixtures/Experiments/ golden experiment JSON files
    PlayMode/        LabKit.PlayMode.Tests   (few smoke tests)
```
The existing `Assets/Scripts/` (`CubeMover.cs`, `NewAssembly.asmdef` with `defineConstraints: ["Test"]`) is a throw-away test. Remove it in the first Core task.

### Layers and allowed dependencies
| Assembly | May reference | Must NOT reference |
|---|---|---|
| `LabKit.Core` | nothing (Newtonsoft only, see ADR-008) | UnityEngine, any other LabKit assembly |
| `LabKit.Net` | Core | Lab, Authoring, Quest |
| `LabKit.Lab` | Core | Net, Authoring, Quest, XR packages |
| `LabKit.Authoring` | Core, Net, Lab | Quest |
| `LabKit.Quest` | Core, Net, Lab, XR packages | Authoring |
| `LabKit.Editor` | any (Editor only) | referenced by none |
| `LabKit.Core.Tests` | Core | Lab and above |

### Builds (ADR-001)
| Build | Platform | Scenes | Assemblies active |
|---|---|---|---|
| `Authoring-Windows` | Windows standalone | `Authoring_Main`, `Lab_Sandbox` | Core, Net, Lab, Authoring |
| `Runtime-Quest` | Android | `Quest_Main` | Core, Net, Lab, Quest |

Selected through Unity **Build Profiles** (owner tested define constraints per profile; scene list per profile UNVERIFIED: SP-2). Fallback: two Editor menu items in `LabKit.Editor` that build an explicit scene list for an explicit target. Switching platform reimports assets: do daily work on Windows, switch to Android only for headset builds.

## 5. Core model in one page

The **simulation is plain C#, deterministic, with no UnityEngine dependency** (ADR-002). It can run in tests, in the authoring app (verification) and in both builds (play).

| Concept | Meaning |
|---|---|
| Catalog | Reviewed definitions: substances, containers, tools, rule data, consequence types. JSON files (ADR-008). Also sent to the AI as the allowed vocabulary. |
| `WorldState` | Containers, each with contents = list of (substanceId, amountMl) and temperatureC. |
| `LabAction` | Data describing what the player does: `Pour`, `Stir`, `Heat`, `Measure`. Used by input, reference solution, probes. |
| `Simulation` | `Apply(LabAction)` and `Advance(dtSeconds)`. Emits `SimEvent`s (for example `TemperatureChanged`, `Splash`, `BoilOver`). No randomness, no wall-clock time. |
| Rule family | Generic mechanism driven by data tables: `MixingHeat`, `Neutralization`, `Threshold` (first-release cap: **2 or 3 families**, chosen by the first experiment). |
| Objective | Declarative conditions over state and events, for example "container B holds X within range and no `Splash` occurred". |
| Experiment | Initial state + objective + hint triggers + (reference solution + mistake probes, used for hints and verification only). |
| Rule card | Readable view of a catalog rule: what it models, assumptions, supported range, **source**, review status, cross-validation badge. Authored data, **never AI text** (ADR-004). |

### Experiment JSON (sketch; final schema defined in the Core tech-spec)
```json
{
  "schemaVersion": 1,
  "id": "exp-0001",
  "title": "...",
  "summary": "...",
  "setup": { "containers": [ { "id": "b1", "kind": "beaker250", "contents": [ { "substance": "water", "amountMl": 100 } ] } ] },
  "objective": [ { "type": "contentRange", "container": "b1", "substance": "...", "minMl": 0, "maxMl": 0 } ],
  "hints": [ { "when": { "type": "event", "event": "Splash" }, "text": "..." } ],
  "referenceSolution": [ { "type": "pour", "from": "...", "to": "b1", "amountMl": 10 } ],
  "mistakeProbes": [ { "name": "...", "actions": [ ], "expectEvent": "Splash" } ]
}
```
Polymorphic items use an explicit `"type"` discriminator (ADR-008). The Author returns a wrapper `{ "status": "ok" | "refused", "experiment": {...}, "refusal": { "reason": "...", "alternatives": [ ] } }`.

## 6. Data flow

```
Teacher text
   |  (Authoring app: chat screen)
   v
Server /generate  --(catalog ids + schema + optional stored experiment as context)--> Claude
   |  <-- JSON (status ok | refused)
   v
Authoring app:  schema + semantic validation (Core)
   -> headless Verifier (Core): reference solution reaches objective? each mistake probe fires its event?
   -> if failed: send error list back to /generate (max 2-3 repair tries)
   -> Review screens: summary, setup, rule cards (looked up in catalog), verification report
   -> Preview (Lab scene, keyboard input)  -> teacher OK
   v
Server /experiments  --> short code
   v
Quest app: enter code -> GET /experiments/{code} -> re-validate (Core) -> build Lab scene -> play with controllers
```
Development without the server: `MockAuthor` returns recorded experiments; local-file source loads JSON. The public repo runs fully offline this way.

## 7. Key decisions

| ADR | Decision |
|---|---|
| [001](decisions/ADR-001-one-project-two-builds.md) | One Unity project, two builds, assembly-definition layering |
| [002](decisions/ADR-002-rule-driven-simulation.md) | Rule-driven simulation (level B): AI composes setup, authored rules own the physics |
| [003](decisions/ADR-003-offline-reference-and-crossval.md) | Scientific engines used offline; cross-validation by committed fixtures |
| [004](decisions/ADR-004-ai-composes-never-authors-rules.md) | AI picks IDs, never writes rules or sources; refusal; verify-and-repair loop |
| [005](decisions/ADR-005-tiny-server.md) | Tiny server: AI proxy, experiment storage and memory |
| [006](decisions/ADR-006-public-repo-private-deploy.md) | Public repo with server code; private sibling repo; secrets policy |
| [007](decisions/ADR-007-constructor-injection.md) | Plain constructor injection, no DI container |
| [008](decisions/ADR-008-data-formats.md) | Newtonsoft with discriminator; catalog as JSON |
| [009](decisions/ADR-009-test-strategy.md) | Test strategy: Core-heavy, golden files, recorded AI responses |
| [010](decisions/ADR-010-input-layers-preview-xr.md) | Input abstraction, desktop preview, XR controllers first |
| [011](decisions/ADR-011-trust-signals-ratings-deferred.md) | Trust signals now; community ratings deferred |

Other documents: [coding-standards](coding-standards.md), [patterns](patterns.md), [dev-workflow](dev-workflow.md), [server-api](server-api.md).

## 8. Risks and time-boxed spikes

Hand to the owner to schedule with the project-manager (the architect does not edit the PM backlog).

| ID | Spike | Time | When | Question |
|---|---|---|---|---|
| SP-1 | Unity version | 0.5 d | Before M1 | Is 6000.6.5f1 stable enough, or move to an LTS? XRI / Meta OpenXR versions for it? |
| SP-2 | Build profiles | 0.5 d | Before M1 | Does a profile hold its own scene list and defines? Else use the Editor-script fallback. |
| SP-3 | Newtonsoft | 0.5 d | Before M1 | Installs on this Unity; referenced from a `noEngineReferences` asmdef; discriminator converter round-trip; IL2CPP/Android stripping (`link.xml`) tested again on device in SP-5. |
| SP-4 | Reference source | 1 d | After experiment chosen | Can PHREEQC (Python) or a published table give reference values for the first experiment's data? PHREEQC may be weak for concentrated acid (UNVERIFIED). |
| SP-5 | Quest basics | 1-2 d | Headset arrives | HTTPS fetch on device, XRI version works, perf baseline at 72 fps, IL2CPP JSON. |
| SP-6 | Server hosting | 1 d | Before M4 | Language and host; secrets handling; HTTPS; rate limiting. |
| SP-7 | AI schema | 0.5 d | Before M2 real AI | Which schema features the structured-outputs mode accepts (unions/discriminators?), which model, cost per generation. The Core validator remains the real guard. |

Other risks:
| Risk | Mitigation |
|---|---|
| AI quality: invalid or unsafe experiments | Catalog vocabulary, validation, headless verification, repair loop, refusal path, rule cards (ADR-004) |
| Chemistry correctness | Sources on every value, cross-validation fixtures, `Unreviewed` status shown honestly (ADR-003) |
| Content cost of consequences (VFX) | Cap at 2-3 consequence types in the first release |
| No headset until about 2026-10-28 | Work order M1-M4 needs none; M5 is the first on-device milestone |
| Public server abuse and cost | Token, rate limit, size cap, spend limit at the provider (UNVERIFIED availability), re-validation on every client (ADR-005) |
| Secret leak in public repo | ADR-006 |

## 9. Provisional milestones (to be mapped to PM IDs)

| # | Milestone | Needs headset |
|---|---|---|
| M0 | Spikes SP-1 to SP-3 | No |
| M1 | `Core`: model, catalog, simulation, 2-3 rule families, validator, verifier, tests, hand-written experiment JSON | No |
| M2 | Authoring app: chat, review screens, rule cards, verification report, `MockAuthor` (recommend pulling the local server + real Claude here as soon as the schema is stable; prompt quality is the biggest unknown on this side) | No |
| M3 | `Lab` scene + keyboard preview (also the dev sandbox) | No |
| M4 | Server (local, then hosted), store/fetch by code, real AI in the demo flow | No |
| M5 | Quest runtime: XR grab, tilt-to-pour, hints, fetch by code | **Yes** |

## 10. Non-goals (for now)

- A real chemistry engine inside the player.
- Full molecular or fluid simulation (pouring is a particle effect + numbers).
- Voice input, hand tracking, multi-user, accounts, community ratings.
- Public playable build; cloud scaling.
- A DI framework, event-bus frameworks, UniTask, ECS.
- Teacher-editable rules (teachers adjust setup through chat only).

## 11. Open questions

| # | Question | Owner of the answer |
|---|---|---|
| Q1 | Which first experiment and education level? Drives the brick list and SP-4. | Owner |
| Q2 | School vs museum framing. | Owner / PM |
| Q3 | Server language and host (SP-6). | Owner + architect |
| Q4 | Who is the reviewer for rule cards (owner, a teacher friend)? | Owner |
| Q5 | License of the public repo. | Owner |

## 12. Scope changes to take to the project-manager

The brainstorm said "no full desktop simulation". The owner now wants (a) a **playable PC preview** inside the authoring app, (b) the **server** as AI proxy + storage + memory, (c) the **public** repo including server code. All three are reflected here and are scope additions the PM must register.

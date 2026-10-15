# ADR-011: Newtonsoft JSON with explicit discriminator; content as JSON files

Status: Accepted (2026-10-15). Package versions UNVERIFIED (SP-3). Carried over from Lab Kit ADR-008, adapted.

## Context
Specs, params and API payloads are polymorphic (per exercise family). `JsonUtility` has no polymorphism or dictionaries. `Core` has no UnityEngine reference, so it cannot use ScriptableObjects. The server needs the same content as the client.

## Options
| Option | Verdict |
|---|---|
| `JsonUtility` | Rejected: cannot model the schema. |
| `System.Text.Json` | Rejected: not available in Unity's netstandard2.1 profile by default (UNVERIFIED). |
| Newtonsoft with `TypeNameHandling` | Rejected: security risk on downloaded or AI-produced JSON. |
| **Newtonsoft with an explicit `"family"` / `"type"` field and custom converters** | **Chosen** |
| Content as ScriptableObjects | Rejected for Core data: not readable by pure C#, not diffable, not sendable to the AI or server. |

## Decision
- All specs, content and API payloads use Newtonsoft (`com.unity.nuget.newtonsoft-json` in Unity, `Newtonsoft.Json` NuGet on the server) with explicit discriminators. Unknown discriminator = validation error.
- Content in `Assets/_Project/Data/Content/`: `skills.json`, `bricks.json`, `facts.json`. Loaded by `Core` from strings. The server reads the same files from a configured path (copied on deploy).
- ScriptableObjects only map content ids to presentation (prefab, color, icon) in `Data/Presentation/`.
- `schemaVersion` on specs and content; loaders reject unsupported versions.
- IL2CPP/WebGL may strip reflection-used code: `link.xml`, tested in SP-4 and SP-5.
- Units: millilitres (mL), litres (L), grams (g), g/L, mol, seconds; the unit is a suffix in field names (`TargetVolumeMl`).

## Consequences
- Diffable, reviewable content; one vocabulary shared by client, server, AI and tests.
- Whether Newtonsoft is accepted by a `noEngineReferences` asmdef is checked in SP-3; fallback: a small `Tutor.Core.Json` adapter assembly.

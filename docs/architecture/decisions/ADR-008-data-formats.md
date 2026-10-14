# ADR-008: Newtonsoft JSON with explicit discriminator; catalog as JSON files

Status: Accepted (2026-10-14). Package version UNVERIFIED (SP-3).

## Context
Experiments, objectives and actions are polymorphic (several condition and action types). Unity's `JsonUtility` has no polymorphism or dictionaries. `Core` has no UnityEngine reference, so it cannot use ScriptableObjects.

## Options
| Option | Verdict |
|---|---|
| `JsonUtility` | Rejected: cannot model the schema. |
| Newtonsoft with `TypeNameHandling` | Rejected: security risk on downloaded files. |
| **Newtonsoft (`com.unity.nuget.newtonsoft-json`) with an explicit `"type"` field and custom converters** | **Chosen** |
| Catalog as ScriptableObjects | Rejected for Core data: not readable by pure C#, not diffable on GitHub, not sendable to the AI. |
| **Catalog as JSON files** under `Assets/_Project/Data/Catalog/` | **Chosen** |

## Decision
- All experiment, catalog and API payloads use Newtonsoft with `"type"` discriminators; unknown type = validation error.
- `LabKit.Core` references Newtonsoft through the asmdef (override references). Whether this works with `noEngineReferences` is checked in SP-3; if not, Newtonsoft sits only in a small `LabKit.Core.Json` adapter and the model stays plain.
- Catalog JSON: substances, containers, tools, rule data, consequence types, rule-card text (what, assumptions, range, `source`, `reviewStatus`). Loaded by `Core` from strings.
- ScriptableObjects only map catalog IDs to presentation (prefab, color, VFX) in `Data/Presentation/`.
- `schemaVersion` field on experiments; the loader rejects unsupported versions.
- Android IL2CPP may strip reflection-used code: test on device (SP-5), add `link.xml` if needed (UNVERIFIED).

## Consequences
- Diffable, reviewable data; one vocabulary shared by app, AI and tests.
- Unit conventions: millilitres, °C, mol/L, grams, seconds; suffix in field names.

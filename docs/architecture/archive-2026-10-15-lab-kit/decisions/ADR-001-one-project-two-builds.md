# ADR-001: One Unity project, two builds, assembly-definition layering

Status: Accepted (2026-10-14)

## Context
Two apps (Windows authoring, Quest runtime) share the experiment schema, catalog, simulation and 3D presentation. Owner has never built two targets from one project.

## Options
| Option | Verdict |
|---|---|
| Two Unity projects | Rejected: schema, catalog and simulation would be duplicated or shared through a package; double maintenance for one developer. |
| **One project, two builds** (Build Profiles + assembly definitions) | **Chosen** |
| Single app with a mode switch | Rejected: ships XR code in the desktop build and desktop UI in VR; blurs layers. |

## Decision
- One project. Assemblies: `Core`, `Net`, `Lab`, `Authoring`, `Quest`, `Editor` (+ tests), see `architecture-overview.md` section 4.
- `Authoring` is limited to Editor + Windows, `Quest` to Editor + Android, via asmdef platform filters. A build contains only its own scenes.
- Build selection by Unity Build Profiles (`Authoring-Windows`, `Runtime-Quest`). Fallback if profiles cannot hold the scene list or defines: Editor menu items in `LabKit.Editor` calling `BuildPipeline` with explicit scenes and target.
- Daily work on Windows; switch to Android only for headset builds (platform switch reimports assets).

## Consequences
- The compiler blocks `Quest` code from leaking into `Authoring` and the reverse.
- Open: scene list per profile is UNVERIFIED (SP-2).
- Command-line builds need the profile or target on the command line (Unity docs: https://docs.unity3d.com/6/Documentation/Manual/build-command-line.html, accessed 2026-10-14).

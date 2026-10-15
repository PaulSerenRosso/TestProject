# ADR-001: One Unity project, one app, two shells, assembly-definition layering

Status: Accepted (2026-10-15). Scene list per Build Profile UNVERIFIED (SP-2). Replaces Lab Kit ADR-001.

## Context
The student app must run on PC (browser) and on Quest with the same exercises, checker and profile. Only input, UI shell and some presentation differ. The owner has never built two targets from one project.

## Options
| Option | Verdict |
|---|---|
| Two Unity projects | Rejected: core logic and content duplicated or shared through a package; double maintenance for one developer. |
| **One project, two shells** (Build Profiles + assembly definitions) | **Chosen** |
| One scene with a runtime mode switch | Rejected: ships XR code in the web build and blurs layers; WebGL has no XR. |

## Decision
- One project. Assemblies: `Core`, `Net`, `Lab`, `Web`, `Quest`, `Editor` (+ tests); see `architecture-overview.md` section 5.
- `Web` is limited to WebGL + Editor, `Quest` to Android + Editor, by asmdef platform filters. A build contains only its own scenes.
- Build selection by Unity Build Profiles (`Web-WebGL`, `Quest-Android`). Fallback if profiles cannot hold the scene list or defines: Editor menu items in `Tutor.Editor` calling `BuildPipeline` with explicit scenes and target.
- Daily work on Windows/WebGL; switch to Android only for headset builds (platform switch reimports assets).

## Consequences
- The compiler blocks Quest code from leaking into Web and the reverse.
- Almost all logic sits in `Core`, so a shell is small. A new brick works on both platforms by default; "VR adds nothing" bricks stay web-only (concept rule).

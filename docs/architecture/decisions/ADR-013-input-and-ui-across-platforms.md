# ADR-013: Same logic, per-shell input and UI; UI technology by spike

Status: Accepted (2026-10-15), UI technology open (SP-8). Adapted from Lab Kit ADR-010. XR package versions UNVERIFIED (SP-1, SP-5).

## Context
Web and VR have equal weight and the same exercises. Number entry, menus and tutor panels exist on both; 3D manipulation (dilution bench) exists in both with different input. Headset arrives about 2026-10-28.

## Decision
- Three layers: **Logic** (`Core`: `ExerciseSession` state, `ExerciseInstance`, `StudentAction`), **Presentation** (`Lab` for 3D; shell screens), **Input** (turns intent into actions or answers).
- Web: mouse/keyboard + screens. Quest: XR Interaction Toolkit and OpenXR actions through the Input System, never device-specific code. Both feed the same `Core` API.
- Number entry in VR: a world-space keypad (no keyboard typing). Login in VR: pairing code (ADR-005).
- **UI technology:** default is UI Toolkit on Web and uGUI world-space on Quest. If SP-8 shows world-space UI Toolkit works with XRI on this Unity version, use UI Toolkit for both and extract a shared `Tutor.Ui` assembly. Do not build shared screens before SP-8.
- **Controllers only** in v1. Comfort: bench scale, no locomotion, no forced camera movement.
- Every brick answers "what does VR add over PC?" in its spec; if "nothing", it is web-only and says so.
- Optional later: XRI's simulator to test the XR rig without a headset (https://docs.unity3d.com/Packages/com.unity.xr.interaction.toolkit@3.5/manual/index.html, accessed 2026-10-14).

## Consequences
- XR work shrinks to mapping gestures to `StudentAction`s; the rest is tested on the web first.
- Two UI stacks are a real cost until SP-8 says otherwise.

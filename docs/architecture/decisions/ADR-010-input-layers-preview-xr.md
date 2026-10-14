# ADR-010: Input abstraction, desktop preview, XR controllers first

Status: Accepted (2026-10-14). XR package versions UNVERIFIED (SP-1, SP-5).

## Context
Headset arrives about 2026-10-28. The owner wants to test interactions by keyboard first and offer a playable PC preview to the teacher.

## Decision
- Three layers: **Simulation** (`Core`, knows only `LabAction`s), **Presentation** (`Lab`: 3D objects, VFX, listens to `SimEvent`s), **Input** (turns player intent into `LabAction`s).
- Input implementations: keyboard/mouse in `LabKit.Authoring` (for example hold a key to tilt a bottle, tilt angle sets pour rate); XR in `LabKit.Quest` (grab, tilt-to-pour, snap) through XR Interaction Toolkit and OpenXR actions via the Input System, never device-specific code. Both feed the same simulation API.
- The **Lab preview** is the `Lab_Sandbox` scene inside the authoring build, driven by keyboard input. It doubles as the developer sandbox. If time runs short, fall back to a step-through replay of the verified reference solution; architecture unchanged.
- **Controllers only** in v1. Hand tracking (pouring, turning and snapping with bare hands is risky) is deferred: reconsider after on-device testing.
- Comfort: lab-bench scale, no locomotion, no camera movement forced by the app.
- VR hints UI: uGUI world-space canvas.
- Optional later: XRI's simulator (named "XR Device Simulator" in older versions, "XR Interaction Simulator" in 3.4+; docs https://docs.unity3d.com/Packages/com.unity.xr.interaction.toolkit@3.5/manual/index.html, accessed 2026-10-14) to test XR rigs without a headset.

## Consequences
- XR work shrinks to mapping physical gestures to `LabAction`s; the rest is tested before the headset arrives.
- Authoring build contains 3D content, so it is larger than a pure UI app.

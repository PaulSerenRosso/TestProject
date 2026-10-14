# ADR-004: The AI composes setups, never writes rules or sources

Status: Accepted (2026-10-14)

## Context
Unchecked AI content on hazardous topics is the main trust risk. A hallucinated source looks as credible as a real one.

## Decision
- The AI receives the catalog vocabulary (IDs) and the JSON schema, and returns an Author result: `status: ok | refused`. For `refused`: `reason` and `alternatives`.
- The AI chooses and parameterizes bricks only: containers, substances, amounts, objective, hints, reference solution, mistake probes. It **never** writes rule text, sources, review status or physics.
- **Rule cards are authored data.** The app lists the cards relevant to an experiment by looking up rules whose substances and conditions appear in the setup (pure function in `Core`).
- **Verify-and-repair loop** (in the authoring app, using `Core`):
  1. schema + semantic validation (IDs exist, references resolve, ranges sane);
  2. run the reference solution headlessly: objective reached?
  3. run each mistake probe: expected event fired?
  4. on failure, send the error list plus the previous attempt back for repair, max 3 tries; then show the failure to the teacher.
- Structured outputs constrain the shape, but **the C# validator is the real guard** (provider schema subset UNVERIFIED, SP-7).
- Teacher reviews summary, setup, rule cards and verification report before preview and publish. Teachers adjust through chat, not by editing rules.

## Consequences
- Verification evidence is shown in the UI: a portfolio highlight.
- Needs a deterministic simulation (ADR-002) and the mock author (ADR-009) for tests.
- Prompt quality is the main unknown; record real responses as test fixtures.

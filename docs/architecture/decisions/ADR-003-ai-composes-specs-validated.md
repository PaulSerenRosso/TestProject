# ADR-003: The AI composes specs and explanations; code validates; seeded fallback

Status: Accepted (2026-10-15). Replaces Lab Kit ADR-004. SP-7 open (schema limits, model, cost).

## Context
The owner wants the AI to generate exercises, answer student questions, adapt difficulty and regenerate on request, with **automatic validation**. Unchecked AI content shown to teenagers is the main trust risk. A free-form exercise cannot be auto-verified; a parametrized one can.

## Options
| Option | Verdict |
|---|---|
| AI writes complete exercises including the answer | Rejected: nothing to verify against. |
| AI only picks a premade exercise | Rejected by owner: wants generation. |
| **AI fills an `ExerciseSpec` (parameters, story, hints, fact ids) for a family; code computes every answer** | **Chosen** |
| AI also chooses the next skill | Deferred (Q9). Code (`TutorPolicy`) decides: testable, free, deterministic. The AI's value is variety and explanation. Easy to flip later since the policy output is just a request to the composer. |

## Decision
- The AI receives the allowed vocabulary (family ids, parameter ranges, skill ids, fact ids) and the JSON schema, plus the requested skill and difficulty from the policy. It returns an `ExerciseSpec`. It **never** returns an answer, a formula, a fact or a source.
- Text fields are **templates**; numbers appear only through placeholders filled by code, and the validator rejects digits in free text. A statement cannot contradict its numbers.
- **Validate-and-repair loop on the server:** (1) `ExerciseSpecValidator` (schema, family, ranges, answer computable and sane, difficulty in the band, wrong-rule answers distinct, placeholders, ids, safety word list); (2) on failure send the diagnostics back, max **2** repairs; (3) still failing: `SeededComposer`. A student is never blocked by an AI failure.
- Explanations and answers to questions: structured result `status: answer | refused | out_of_scope` with `factIds`. `AnswerGuard` requires existing fact ids for `answer`. Questions outside the fact sheet and "how do I make..." requests are refused with "ask your teacher". The AI never judges a student answer; code does.
- Validated specs are stored in an exercise bank and may be reused for other students (saves tokens).
- **Limit stated honestly:** the guard proves structure and grounding ids, not that explanation prose is faithful to the facts.

## Consequences
- The verification evidence (how often the AI needed repair, how often it fell back) is demo material.
- Needs a mock AI and recorded responses for tests (ADR-012).
- Prompt quality is the biggest unknown; record real responses as fixtures.

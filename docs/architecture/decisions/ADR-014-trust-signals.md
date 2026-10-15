# ADR-014: Trust signals now; ratings and teacher dashboard deferred

Status: Accepted (2026-10-15). Carried over from Lab Kit ADR-011, adapted.

## Context
Students, teachers and portfolio viewers must be able to trust the chemistry and see how the AI is kept in check.

## Options
| Option | Verdict |
|---|---|
| Community ratings and comments per brick | Deferred: needs moderation, spam control and more accounts logic; no story needs it. |
| Teacher dashboard (error tags per class) | Deferred to M7: needs classes and consent logic; the attempt log already holds the data. |
| **Authored trust signals** | **Chosen** |

## Decision
Every brick and fact shows (available in an "about this exercise" panel):
- **Source** (programme line, textbook, table) authored by the owner, never AI text.
- **Review status:** `Reviewed by <role>, <date>` or `Unreviewed`, stored in the content files. Everything not reviewed by a teacher shows `Unreviewed`.
- **Origin of the exercise:** `code-generated` or `AI-composed and code-verified`.
- **Supported range / assumptions** where relevant.
- **"Report an issue" link** that opens a GitHub Issue prefilled with the brick or fact id (GitHub provides accounts and moderation; no backend work).
- No in-app review workflow and no ratings.

## Consequences
- Honest and cheap; the AI/code split is visible to the user.
- Revisit ratings or a teacher view only with a PM story and an authentication decision.

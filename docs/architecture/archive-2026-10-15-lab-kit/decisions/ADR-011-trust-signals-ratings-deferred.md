# ADR-011: Trust signals now; community ratings deferred

Status: Accepted (2026-10-14)

## Context
The owner wants visitors and teachers to trust the chemistry. Idea raised: stars and comments on rules.

## Options
| Option | Verdict |
|---|---|
| Community ratings and comments per rule | Deferred: needs accounts, moderation, spam protection, database; no story needs it; unverifiable star counts weaken trust. |
| **Authored trust signals** | **Chosen** |

## Decision
Every rule card shows:
- **Source** for rules and values (authored by the owner).
- **Cross-validation badge** from fixture metadata (ADR-003), or `Not cross-validated`.
- **Review status**: `Reviewed by <name>, <date>` or `Unreviewed`, stored in the catalog data. First release: one reviewer (owner or a teacher friend); everything else shows `Unreviewed`.
- **Supported range** and assumptions.
- **"Report an issue" link** opening a GitHub Issue prefilled with the rule ID. GitHub provides accounts and moderation; no backend.
- No in-app review workflow, no accounts.

## Consequences
- Honest and cheap. Revisit ratings only with a PM story and a decision on authentication.

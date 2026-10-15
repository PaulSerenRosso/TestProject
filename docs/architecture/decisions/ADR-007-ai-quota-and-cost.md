# ADR-007: Daily AI credits per account, global cap, graceful fallback

Status: Accepted (2026-10-15). Numbers are ASSUMPTIONS (Q7). Cost per call UNVERIFIED (SP-7).

## Context
The server spends money on every AI call, and the public repo shows how it works. The owner wants a daily limit per student so tokens cannot be spammed.

## Decision
- **Credits:** each account has a daily budget (ASSUMPTION: 20). Costs: AI exercise 1, regeneration 1, question 1. Repair retries inside one generation are free for the student but capped at 2 per generation and counted in the global cap.
- `QuotaPolicy` (pure, in `Core`, tested) holds costs and the limit; the server enforces it **atomically** in the DB (`ai_usage(student, day)` row) before calling the AI.
- Reset boundary: midnight in a configured time zone (ASSUMPTION `Europe/Paris`).
- **Exhausted credits:** exercises come from `SeededComposer` or the exercise bank (labeled "practice mode"); questions return `quota_exhausted` with `resetsAt`. The app stays usable.
- **Global cap:** daily credit ceiling for the whole server and a spend limit at the AI provider (availability UNVERIFIED). Registration gated by invite code (Q6).
- Other abuse controls: rate limit per token, request body cap (16 KB), question cap (300 characters), `max_tokens` cap on every AI call.
- Every response carries `quota { remaining, resetsAt }` so the UI can show it.

## Consequences
- Cost has a hard upper bound: accounts x credits x average call cost.
- The bank of validated specs lowers cost as it grows.
- The limit is also a gamification hook (daily AI "energy"); design belongs to the PM.

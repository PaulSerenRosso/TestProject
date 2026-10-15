# ADR-006: Pseudonymous accounts, summary-only storage, no chat storage

Status: Accepted (2026-10-15). Not legal advice; real use with minors needs a GDPR / EU AI Act review (concept note section 9).

## Context
The owner wants cross-device memory in the cloud while "never storing real personal data". The demo uses test accounts only. Free-text questions from teenagers may contain personal information.

## Decision
- **Identity** = pseudonym + password hash. No name, no email, no birth date, no IP stored with attempts. Pseudonym is server-generated (ASSUMPTION, Q5) or a chosen one with a "no real name" rule.
- **Stored per account:** attempts (exercise id, answer, correct, error tag, hints used, duration, timestamp), a derived profile summary (mastery per skill, top error tags, XP, streak), AI credit counter per day. Nothing else.
- **Never stored or logged:** student questions, AI answers, prompts, raw AI responses (outside tests with fake data). Server request logging excludes bodies of `/tutor/ask`. A test asserts that the schema has no chat column.
- Questions are capped at 300 characters, shown with "do not write personal information", and sent to the AI provider without the pseudonym.
- **Delete and export:** `DELETE /me` removes all rows of the account; `GET /me/export` returns them as JSON.
- Password recovery does not exist (no email); the owner resets test accounts by hand. Accepted for a demo.
- Provider settings (EU region, no training on data, zero retention) are UNVERIFIED (SP-7). Test values only until they are confirmed.

## Consequences
- Privacy can be explained in three sentences in the README.
- Without email there is no recovery and no direct teacher link; both are deliberate.
- Retention and compaction of old attempts are deferred (note for the server tech-spec).

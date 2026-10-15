# Server API contract (DRAFT)

Status: Draft, 2026-10-15. `server/Tutor.Server` implements it; `Tutor.Net` consumes it. Final shapes are fixed in the tech-spec of the story that builds each endpoint. Hosting open (SP-6). Replaces the Lab Kit contract.

## Conventions
- HTTPS (plain HTTP only on localhost), JSON, UTF-8. Header `Authorization: Bearer <jwt>` on every call except `/auth/register`, `/auth/login`, `/auth/pair`.
- Errors: `{ "error": { "code": "string", "message": "string" } }` with an HTTP status. Quota: HTTP 429, code `quota_exhausted`, extra field `resetsAt`.
- Every learning response carries `quota: { "remaining": int, "resetsAt": "ISO-8601" }`.
- Limits (ASSUMPTION): body 16 KB; question 300 characters; rate limit per token; `max_tokens` cap on AI calls.
- The server holds the AI key and JWT signing key in its environment only.
- Payload types are the `Core` types (`ExerciseSpec`, `Attempt`, `ProfileSummary`) serialized with ADR-011 rules.
- The server never logs request bodies of `/tutor/ask` and never stores them (ADR-006).

## Endpoints
| Method and path | Purpose | Request | Response |
|---|---|---|---|
| `POST /auth/register` | Create an account (invite-gated, Q6) | `{ "inviteCode", "password" }` | `{ "pseudonym", "token", "expiresAt" }` (pseudonym server-generated, Q5) |
| `POST /auth/login` | Sign in | `{ "pseudonym", "password" }` | `{ "token", "expiresAt" }` |
| `POST /auth/pairing` | Create a short-lived code on the web app (M6) | none | `{ "code", "expiresAt" }` |
| `POST /auth/pair` | Headset exchanges the code for a token (M6) | `{ "code" }` | `{ "token", "expiresAt" }` |
| `GET /me/summary` | Profile summary for the home screen | none | `{ "pseudonym", "masteryBySkill", "topErrorTags", "xp", "level", "streakDays", "quota" }` |
| `GET /me/export` | Export all stored data (ADR-006) | none | JSON of attempts + summary |
| `DELETE /me` | Delete the account and all rows | none | 204 |
| `POST /exercises/next` | Next exercise (policy picks skill and difficulty) | `{ "preferredSkillId": "optional" }` | `{ "exerciseId", "source": "ai" \| "seeded" \| "bank", "spec": {..}, "quota" }` |
| `POST /exercises/regenerate` | Another variant of the same skill and difficulty (costs a credit) | `{ "exerciseId" }` | same as `next` |
| `GET /exercises/{id}` | Fetch a stored spec (resume) | none | `{ "exerciseId", "spec": {..} }` |
| `POST /attempts` | Submit an answer; idempotent by `attemptId` | `{ "attemptId": "guid", "exerciseId", "answer", "hintsUsed", "durationMs" }` | `{ "result": { "correct", "errorTag", "expected" }, "summary": {..}, "quota" }` |
| `POST /tutor/ask` | Ask a question, optionally about the current exercise | `{ "exerciseId": "optional", "question" }` | `{ "status": "answer" \| "refused" \| "out_of_scope", "text", "factIds": [..], "quota" }` |

## Rules
- The server builds the prompt: system instructions + vocabulary (families, ranges, skills, fact sheet) + the policy's request. No embeddings, no memory of past chats.
- `POST /exercises/next` always succeeds with a valid spec: AI -> validate -> repair (max 2) -> `SeededComposer`. `source` tells which path produced it.
- The server re-checks each attempt with `Core` and stores its own result; the client's local feedback is only a convenience.
- Mock-AI mode (env flag) returns recorded specs and answers so the whole chain runs without a key.
- Pseudonyms are not secrets but are not listed anywhere; no endpoint enumerates accounts.
- Pairing codes: single use, about 5 minutes, unguessable enough for a demo (about 8 characters).

# Server API contract (DRAFT)

Status: Draft, 2026-10-14. The server (`server/`) implements it; clients (`LabKit.Net`) consume it. Final shapes are fixed in the tech-spec of the story that builds the server. Language and host are open (SP-6).

## Conventions
- HTTPS, JSON, UTF-8. Header `Authorization: Bearer <token>` on every call except `GET /experiments/{code}` (short code is the access key for the headset).
- Errors: `{ "error": { "code": "string", "message": "string" } }` with an HTTP status.
- Limits (ASSUMPTION): request body 256 KB; rate limit per token; stored experiment max 128 KB.
- The server holds the AI key in its environment only. Clients never see it.

## Endpoints
| Method and path | Purpose | Request | Response |
|---|---|---|---|
| `POST /generate` | Ask the AI for an experiment | `{ "request": "free text", "baseExperimentId": "optional", "previousAttempt": {..optional..}, "errors": [ "optional validation errors for repair" ], "catalogVersion": "string" }` | Author result: `{ "status": "ok", "experiment": {..} }` or `{ "status": "refused", "refusal": { "reason": "...", "alternatives": [ "..." ] } }` |
| `POST /experiments` | Publish a validated experiment | `{ "experiment": {..} }` | `{ "id": "exp-0001", "code": "ABCD-1234" }` |
| `GET /experiments/{code}` | Headset fetches an experiment | none | `{ "experiment": {..} }` |
| `GET /experiments` | List stored experiments (memory / clone) | none | `{ "items": [ { "id", "title", "summary", "createdAt" } ] }` |

## Rules
- The server builds the prompt: system instructions + catalog vocabulary + schema + (optional) base experiment as context. No embeddings.
- The server validates structure and size of what it stores; it does not simulate. Semantic validation and verification happen in the authoring app (`Core`). The Quest app re-validates every download.
- Mock-AI mode (env flag) returns recorded experiments so the whole chain runs without a key.
- Codes: unguessable enough for a demo (about 8 characters, mixed). No accounts.

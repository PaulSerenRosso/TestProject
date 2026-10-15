# ADR-005: ASP.NET Core server with accounts and database, compiling the shared Core

Status: Accepted (2026-10-15). Package versions UNVERIFIED. Hosting open (SP-6). Replaces Lab Kit ADR-005 (tiny server).

## Context
The server now does real work: accounts, a database of profile summaries and an exercise bank, AI proxy with validation, quota. The owner wants it as a portfolio skill (backend, auth, database). The server must run the same validator and checker as the client.

## Options
| Option | Verdict |
|---|---|
| Node/TypeScript or Python server | Rejected: would re-implement the validator and checker (drift risk) or call Unity code through a process. |
| Backend-as-a-service (Firebase, Supabase) | Rejected: hides the backend skills the owner wants to show; AI validation still needs custom code. |
| **ASP.NET Core minimal API on .NET 10 LTS + EF Core + SQLite (Postgres later), compiling the Unity `Core` sources** | **Chosen** |

## Decision
- `server/Tutor.Server` (ASP.NET Core minimal APIs). `server/Tutor.Core.Shared` is a `netstandard2.1` project that **links** the `Core` source files from the Unity folder (no copy) with `LangVersion` pinned to Unity's (SP-3). Contract in `server-api.md`.
- Auth: pseudonym + password (hash with the framework's password hasher), short-lived **JWT bearer** access token. Registration gated by invite code (Q6). Headset login by a short pairing code created on the web app (M6) so nobody types a password in VR.
- Database: EF Core with migrations; SQLite file for dev and demo; Postgres if hosted. Tables: `students`, `invite_codes`, `exercises` (spec bank), `attempts`, `profile_summaries`, `ai_usage`. Schema in the server tech-spec.
- The server **re-checks every attempt with `Core`** and stores its own result. It never trusts client-claimed correctness.
- The Claude key exists only in the server environment (ADR-009). A **mock-AI mode** returns recorded specs and answers.
- The WebGL build is served from `wwwroot`: same origin as the API, no CORS in production (ADR-008).
- Clients are untrusted: rate limit per token, body size caps, quota (ADR-007).

## Consequences
- One validator, one checker, one set of tests for client and server.
- Core code must stay compatible with `netstandard2.1` and Unity's C# version (enforced by the server build).
- More to maintain than a thin pipe; the scope warning in the overview applies.
- A headset cannot reach `localhost`: hosting spike SP-6 before M6.

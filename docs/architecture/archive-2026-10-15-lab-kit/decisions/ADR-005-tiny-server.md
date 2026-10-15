# ADR-005: Tiny server (AI proxy, storage, memory)

Status: Accepted (2026-10-14). Language and host open (SP-6).

## Context
The headset needs a way to receive experiments; the owner wants the authoring app to talk only to the owner's server, and wants previous experiments reusable ("same as this one but...").

## Options
| Option | Verdict |
|---|---|
| USB or file copy | Rejected as main path: Android 12 scoped storage limits (not verified on Quest 2); manual. |
| Authoring app calls Claude directly with a local key; server only stores | Rejected by owner: server also needed for memory, and a cleaner demo. |
| **Server = AI proxy + experiment store + memory** | **Chosen** |

## Decision
- Endpoints (contract in `server-api.md`): `POST /generate`, `POST /experiments`, `GET /experiments/{code}`, `GET /experiments`.
- The Claude key exists only in the server's environment. No client holds it.
- **Memory** = stored experiment JSON passed into the prompt as context ("take this one but..."). No embeddings, no vector database.
- Verification stays in the authoring app (uses `Core`). The server is a thin pipe plus storage; its language is free. It validates only structure and size of what it stores.
- Clients are untrusted: revocable access token, rate limit, request size cap, spend limit at the provider (availability UNVERIFIED). The Quest app re-validates every download with `Core`. Use HTTPS (plain HTTP is blocked by default on Android per general knowledge, UNVERIFIED).
- Dev and tests: server has a **mock-AI mode**; client side has `MockAuthor` and a local-file source behind `IExperimentAuthor` / `IExperimentSource`. Nothing depends on the server being up.

## Consequences
- Server code is public (ADR-006).
- Public endpoint that spends money: abuse control is mandatory before hosting.
- Accounts and per-user storage are out of scope (short code access only).

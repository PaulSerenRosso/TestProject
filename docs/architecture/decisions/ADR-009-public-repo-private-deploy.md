# ADR-009: Public repository with server code; private sibling repo; secrets policy

Status: Accepted (2026-10-15). Carried over from Lab Kit ADR-006, adapted.

## Context
Portfolio goal: show as much code as possible, including the server, without exposing keys or hosting details.

## Options
| Option | Verdict |
|---|---|
| Private folder inside the public repo, ignored by `.gitignore` | Rejected: nested git repo confuses tools and agents; one `git add -f` leaks it. |
| Server in a separate private repo only | Rejected: hides code the owner wants to show. |
| **Public repo (Unity + `server/` + docs); private SIBLING repo for deployment details** | **Chosen** |

## Decision
- Public repo = `D:\Unity\TestProject`. Private repo = `D:\Unity\TestProject-private` (sibling, outside the public tree): deployment notes, hosting config, non-secret infra settings.
- **Real secrets live nowhere in git:** server environment variables or the host's secret store (Claude key, JWT signing key, DB connection string, invite-code seeds). The repo has `.env.example` / `appsettings.Example.json` with placeholders; local config files are gitignored (`.env*`, `*.local.json`, `appsettings.*.local.json`, `secrets/`, `*.db`, `*.sqlite`). The Unity `.gitignore` in `TestUnityProject/` has no such patterns yet: add them, plus a root `.gitignore` for .NET (`bin/`, `obj/`), before the first AI or server work.
- The public project must run **fully offline** (seeded composer, mock-AI mode, SQLite file).
- Safeguards: `main` protected, changes via PR; GitHub push protection (free for public repos, https://github.blog/2023-05-09-push-protection-is-generally-available-and-free-for-all-public-repositories/, accessed 2026-10-14); local pre-push secret scan (tool choice in a tech-spec).
- If a secret is ever committed: assume leaked and **rotate it**.
- Before the first public push: review history, `.claude/`, `docs/brainstorms/` and `docs/chemistry/` for personal data; choose a license (Q10); check third-party asset licenses.

## Consequences
- Assume attackers read the server code: security cannot depend on obscurity (ADR-005, 007).
- The API contract lives in public `server-api.md`.

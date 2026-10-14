# ADR-006: Public repository with server code; private sibling repo; secrets policy

Status: Accepted (2026-10-14)

## Context
Portfolio goal: show as much code as possible, including the server, without exposing keys or hosting details.

## Options
| Option | Verdict |
|---|---|
| Private folder inside the public repo, ignored by `.gitignore` | Rejected as default: nested git repo confuses tools and agents; one `git add -f` leaks it. |
| Server in a separate private repo only | Rejected: hides code the owner wants to show. |
| **Public repo (Unity + `server/` + tools + docs); private SIBLING repo for deployment details** | **Chosen** |

## Decision
- Public repo = `D:\Unity\TestProject`. Private repo = `D:\Unity\TestProject-private` (sibling, outside the public tree): deployment notes, hosting config, non-secret infra settings.
- **Real secrets live nowhere in git**: server environment variables or host secret store. Repo has `.env.example` with placeholders; local config files are gitignored. The Unity `.gitignore` is in `TestUnityProject/` and currently has no secret patterns: add them (and a root `.gitignore`) before the first AI work.
- Server reads all sensitive config from env. Public config holds placeholders.
- The public project must run **fully offline** (mock author, local file source, mock-AI server mode).
- Safeguards: `main` protected, changes via PR; GitHub push protection (free for public repos, source: https://github.blog/2023-05-09-push-protection-is-generally-available-and-free-for-all-public-repositories/, accessed 2026-10-14; private repos may need a paid plan, UNVERIFIED); local pre-push secret scan (tool choice in a tech-spec).
- If a secret is ever committed: assume leaked, **rotate it**; do not rely on history rewrite.
- Before first public push: review history, `.claude/` and `docs/brainstorms/` for personal data; choose a license (open question Q5); check third-party asset licenses.

## Consequences
- Assume attackers can read the server code: security cannot depend on obscurity (ADR-005 controls).
- Two repos to keep in mind; the contract lives in public `docs/architecture/server-api.md`.

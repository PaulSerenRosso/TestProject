# ADR-008: WebGL as the PC target and its coding constraints

Status: Accepted (2026-10-15). Behavior to confirm on this Unity version in SP-4.

## Context
The owner wants the PC version as a WebGL app (even on localhost): no install, matches "practice at home". Unity documents several WebGL limits. Sources (accessed 2026-10-15, search summaries): Unity 6 WebGL technical overview (https://docs.unity3d.com/6/Documentation/Manual/webgl-technical-overview.html), Unity .NET API support (https://docs.unity3d.com/Manual/web-dotnet-api-support.html), WebGL networking (https://docs.unity3d.com/Manual/webgl-networking.html).

## Options
| Option | Verdict |
|---|---|
| Windows standalone | Rejected for the main PC path: install friction, less "home practice". May be a dev convenience. |
| **WebGL served by the ASP.NET Core server** | **Chosen** |
| WebXR for VR in the browser | Rejected: Quest uses a native OpenXR build. |

## Decision
- **No managed threads.** In every assembly that can run in WebGL (`Core`, `Net`, `Lab`, `Web`): no `Thread`, `ThreadPool`, `Task.Run`, `Task.ContinueWith`, `ConfigureAwait(false)`, `Task.Delay`, `System.Threading.Timer`, or `CancellationTokenSource` with a timeout. Use `Awaitable`/coroutines and `UnityWebRequest` timeouts.
- **No `System.Net`** classes. Networking is `UnityWebRequest` only (implemented with the browser Fetch API).
- **CORS:** production serves the build and the API from the same origin. Editor Play Mode and a separately served build need a dev-only CORS policy on the server, off in production.
- **Static files:** the server sets correct `Content-Encoding` and content types for Brotli/gzip Unity builds, or the build uses no compression (SP-4).
- **Stripping:** `link.xml` for Newtonsoft and any reflection-used types; test the real build, not only the Editor.
- **Storage:** `PlayerPrefs` lives in browser storage; the JWT is kept in memory and optionally in `PlayerPrefs` for "stay signed in". No other file I/O (async `FileStream` can hang the browser).
- Desktop browsers only. Size and load-time budget is measured in SP-4.

## Consequences
- The `Core` rule "no threads" already holds, so the shared code runs in the browser.
- Anything heavy must be a server job, not a client thread.
- Quest keeps normal Android capabilities but follows the same rules in shared assemblies.

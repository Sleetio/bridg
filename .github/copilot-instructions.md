<!--
  concise, actionable Copilot / AI-agent instructions for this repository
  ~20-50 lines. Keep examples specific to files in the repo.
-->
# Copilot / AI agent instructions — bridg

This repository is a tiny static site that embeds a BuildMyAgent chat widget and is deployed on Vercel.

Key files
- `index.html` — single-page static site. Includes the BuildMyAgent widget script:
  `https://buildmyagent.io/widget/690ac3b2fe1288edbc85b90a/widget-professional.js?widgetId=690ac3b2fe1288edbc85b90a`.
- `vercel.json` — Vercel configuration for headers/CSP. See `headers[0].headers` for Content-Security-Policy and X-Frame-Options.

Big picture
- No backend code in this repo — it's a static frontend that loads an external chat widget.
- Deployment target: Vercel. The `vercel.json` file controls HTTP headers and CSP; changes to external resources or frames must be reflected there.

What to do when editing
- If you update the widget ID or add other third-party scripts, update `index.html` and verify `vercel.json` CSP/frame-ancestors include their origins.
- Keep changes minimal and self-contained. There is no build step or package.json. For local preview, run a static file server (examples below).

Local preview and verification
- Quick preview (Python):
  - `python3 -m http.server 8000` (run in repo root) then open `http://localhost:8000`.
- If using Vercel CLI for local dev: `vercel dev` (requires installing `vercel` globally and login). The repo has no framework config; `vercel dev` will serve static files.

Network and security notes
- `vercel.json` sets a Content-Security-Policy with `frame-ancestors` entries. If widget or embedded content is blocked, update that header.
- The widget is loaded from `buildmyagent.io` — confirm connectivity when testing locally.

Conventions and PR guidance
- Keep markup simple and inline styles consistent with `index.html` structure.
- For any addition of JS/CSS assets, prefer adding them under the repo root and reference them with relative paths.
- PR checklist for changes affecting runtime:
  - Preview locally with a static server.
  - Verify widget script loads and chat appears in `.chat-container`.
  - Update `vercel.json` headers if adding new external hosts or frame sources.

Examples (use these concrete code locations):
- To change the chat widget, edit the `<script src="...widget-professional.js?..."></script>` line in `index.html`.
- To allow a new iframe host, add it to `vercel.json` `headers[0].headers[1].value`'s `frame-ancestors` list.

If you need to change the project type (add a framework/tooling):
- Add `package.json` and a build script, update `vercel.json` if needed, and include simple start/dev instructions in `README.md`.

If anything in these instructions is unclear or you want me to include additional details (tests, CI, deployment steps), tell me what you'd like clarified and I'll iterate.

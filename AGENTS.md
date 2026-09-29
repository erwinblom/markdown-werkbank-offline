# AGENTS.md

## Project overview

Markdown Werkbank is a **static, client-only** Markdown editor (Dutch UI). No build step, no backend, no server runtime, no package manager. All JS libraries are vendored in `Onderdelen/vendor/`.

## Entry point

The app's single HTML entry point is `▶ Begin hier.html` (note the ▶ and spaces in the filename). It loads scripts and styles from `Onderdelen/`.

## Running in the sandbox

Served by nginx (static files only) via `docker-compose.base44.yml` on port 3000. The nginx config (`nginx.base44.conf`) sets `▶ Begin hier.html` as the index document.

- Start: `docker compose -f docker-compose.base44.yml up -d`
- Health: `curl -sf http://localhost:3000/`
- No migrations, no seeds, no env vars or secrets needed.

## Architecture notes

- Uses the **File System Access API** (`showDirectoryPicker`) — requires a secure context (HTTPS). Works in the preview since it's served over HTTPS.
- CSP is strict (`connect-src 'none'`) — no fetch/XHR/AI calls by design.
- Chrome/Edge desktop are the target browsers; Firefox/Safari/mobile have limited File System Access API support.
- `Werkbank/` contains demo projects (Dutch Markdown files).
- `Onderdelen/tests/` has Playwright smoke tests (`node tests/smoke.cjs`) — dev tooling only, not needed to run the app.

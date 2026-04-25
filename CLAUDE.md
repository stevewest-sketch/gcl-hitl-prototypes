# Claude Code context

## Active file

**`HITL-Task-Prototype-v13.html`** is the working version. Make edits here.
Files in `archive/` are older versions — read only.

## Before editing

1. `git pull` to sync with the remote (Christina may have pushed).
2. Read `docs/PROJECT-MEMORY.md` for current state, decisions, and open threads.
3. Skim `docs/HITL-Feedback.md` for the latest feedback shaping v13.

## Project shape

- Single-file HTML prototype — CSS and JS inline in `HITL-Task-Prototype-v13.html`.
- No build step, no package manager. Opens directly in a browser.
- No external deps beyond CDN scripts already loaded inside the file.
- Vercel auto-deploys on push. `vercel.json` redirects `/` → active version.

## When asked to extend v13

Edit `HITL-Task-Prototype-v13.html` directly. Commit to a feature branch
(`steve/...` or `christina/...`), push, open a PR. Do not commit straight to `main`.

## When asked to start a new major version

1. Copy `HITL-Task-Prototype-v13.html` → `HITL-Task-Prototype-v14.html`.
2. `git mv HITL-Task-Prototype-v13.html archive/`.
3. Update `vercel.json` destination to `/HITL-Task-Prototype-v14.html`.
4. Update this file (`CLAUDE.md`) and `README.md` to reference v14 as active.

## Style

Match the existing Gladly Storybook styles already in the file. Christina keeps
the design system alignment tight — see her commit history for patterns.

## See also

- `README.md` — full setup, workflow, and conventions
- `docs/PROJECT-MEMORY.md` — decisions and history
- `docs/HITL-Feedback.md` — current feedback
- `docs/HITL-Prototype-v7-Walkthrough.md` — narrative walkthrough of v7 flows

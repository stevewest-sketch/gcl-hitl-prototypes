# GCL HITL Prototype

Interactive prototype for Gladly's **Human-in-the-Loop (HITL)** task experience, built
for the **Gladly Connect Live (GCL) 2026** keynote. Single-file HTML — no build step,
no framework. Open any version file in a browser to view.

## Active file

**`HITL-Task-Prototype-v13.html`** is the working version. All new edits land here.
Older versions (v1–v8) are in `archive/` for reference only.

## Live preview

Vercel auto-deploys every push:

- **Production (`main`):** https://gcl-hitl-prototypes.vercel.app (redirects `/` → current active file)
- **Branch previews:** every push to a non-main branch gets its own URL, posted as a comment on the PR

## Run it locally

Clone and open:

```bash
git clone https://github.com/stevewest-sketch/gcl-hitl-prototypes.git
cd gcl-hitl-prototypes
open HITL-Task-Prototype-v13.html          # macOS — opens in default browser
```

Or, if you want live reload while editing, run any static server:

```bash
python3 -m http.server 8000               # then visit http://localhost:8000/HITL-Task-Prototype-v13.html
# or
npx serve .
```

## Folder layout

```
.
├── HITL-Task-Prototype-v13.html   # Active working file — edit this
├── archive/                      # v1–v8, reference only, do not edit
├── docs/                         # Project context
│   ├── PROJECT-MEMORY.md         # Running log of decisions and state (start here)
│   ├── HITL-Feedback.md          # Consolidated feedback across versions
│   ├── HITL-Prototype-v7-Walkthrough.md
│   ├── HITL-Tasks-Analysis-Apr2026.md / .docx
│   └── screenshots/              # Reference screenshots from earlier rounds
├── images/                       # Shared image assets (logo, etc.)
├── vercel.json                   # Redirects / → active version
├── .gitignore
└── README.md                     # You are here
```

## Conventions

**Single-file HTML.** CSS and JS are inline in each `HITL-Task-Prototype-v*.html`.
No build step, no package manager, no external dependencies beyond CDN scripts already
inside the file. Keep it that way unless we explicitly decide otherwise.

**Versioning.** Each major iteration cuts a new version file:

- Small fixes and polish → commit straight to the current version file (e.g. v13).
- Major structural / UX change → copy current version to `HITL-Task-Prototype-v{N+1}.html`,
  move the previous version into `archive/`, and update `vercel.json` so `/` redirects
  to the new active file.

**Commits.** Short, present tense, prefixed with the version. Examples from history:

- `v9: UI polish — icons, layout, avatars, and copilot improvements`
- `v9: Rachel HITL approve flow — action card with steps before execution`

## Contributing

Both of us work on `main` via feature branches and PRs, not direct pushes.

```bash
# Start fresh
git checkout main && git pull

# New branch per piece of work
git checkout -b your-name/what-its-about     # e.g. christina/ui-polish, steve/timeline-empty-state

# ...edit HITL-Task-Prototype-v13.html...

git add HITL-Task-Prototype-v13.html
git commit -m "v13: tightened summary card copy"
git push -u origin your-name/what-its-about

# Open a PR on GitHub (CLI: gh pr create --fill, or use the URL GitHub prints)
```

Vercel will post a **preview URL** on the PR — click it to see your changes live
before merging. Request a review from the other person, then merge when approved.
Delete the branch after merge.

### Staying in sync

Before starting each session:

```bash
git fetch
git checkout main && git pull
```

If your feature branch is behind `main`:

```bash
git checkout your-branch
git rebase main
# resolve any conflicts in v13.html, then:
git push --force-with-lease
```

`--force-with-lease` (not plain `--force`) protects against overwriting someone
else's work on the same branch.

### Conflicts in a single-file prototype

Because everything lives in one `.html` file, overlapping edits conflict hard.
Two habits that keep it manageable:

- **Small, frequent commits.** Easier to rebase and resolve.
- **Rough ownership zones.** If we're both going to touch v13 at the same time,
  agree in Slack on who owns which section (CSS block vs. JS block vs. specific
  component) — or time-box so one person finishes before the other starts.

When a conflict hits: open the file, find `<<<<<<<`/`=======`/`>>>>>>>` markers,
pick or merge the right content, `git add`, `git rebase --continue`.

## Who's working on this

- **Steve West** — Director of Revenue Enablement ([@stevewest-sketch](https://github.com/stevewest-sketch))
- **Christina** — Designer

To add another collaborator: repo → **Settings** → **Collaborators and teams** →
**Add people** → role **Write**.

## Context

Read `docs/PROJECT-MEMORY.md` first — it has the running log of decisions, open
threads, and what each version iteration was trying to solve. `docs/HITL-Feedback.md`
captures consolidated feedback across rounds.

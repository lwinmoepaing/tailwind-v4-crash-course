# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repo is

Lecture code collection for a **Tailwind CSS v4 crash course**. Not one app — a set of small,
standalone snapshots. Students copy **one lecture folder** and run it alone.

## Layout

```
section-<N>/lecture-<M>/
```

Two kinds of lecture folders:

- **Talk-only lecture** — just `README.md` containing `# No Codes` (slides/theory, no demo).
- **Code lecture** — `package.json` + `index.html` + `src/input.css` (output is generated).
  Some also ship a `fonts/` folder (e.g. `section-2/lecture-4`, `lecture-5`); the same font file is
  copied into each lecture on purpose.

Each code lecture is a **complete, self-contained mini project**. It has its own `package.json`
and its own `node_modules`. Keep it that way:

- Do NOT hoist deps to the root, do NOT add workspaces/monorepo tooling.
- Duplicated files between lectures are intentional — each lecture is a snapshot in time.

## Commands

Always `cd` into the lecture folder first (scripts are relative to it):

```bash
cd section-1/lecture-3
npm install
npm run watch    # rebuild CSS on file change (use while teaching)
npm run build    # one-time build
```

Then open `index.html` in a browser.

No tests, no linter. The `test` script is the leftover `npm init` stub and always exits 1 — do not
"fix" it or wire up a test runner.

## Tailwind v4 setup (CSS-first)

v4 has **no `tailwind.config.js`**. Config lives in `src/input.css`:

```css
@import "tailwindcss" source(none);
@source "../index.html";
```

- `source(none)` turns OFF automatic file scanning.
- `@source` then lists the files to scan, one by one.

So if a lecture gains a new HTML file, add another `@source` line, or its classes will be missing
from the built CSS.

Build flow: `src/input.css` → `output/output.css` (generated, not committed), which `index.html`
links via `<link rel="stylesheet" href="output/output.css">`.

## Adding a new lecture

Copy the newest code lecture folder, then edit. Keep `package.json` identical across lectures so
the commands never change for students. (Every `package.json` has `"name": "section-1"` — a
harmless leftover; leave it unless renaming all of them.)

## Git commits

Use **Commitizen / Conventional Commits** style. **One line only — no body.**

```
<type>(<scope>): <short message>
```

- `type` — `feat`, `fix`, `docs`, `style`, `refactor`, `chore`
- `scope` — the lecture folder, e.g. `section-2/lecture-1`. Skip it for repo-wide changes.
- Message in lowercase, present tense, no period at the end.

```
feat(section-2/lecture-1): add invite card layout
fix(section-2/lecture-1): correct output.css path
docs: add readme for students
chore: add gitignore
```

## Gotchas

- `index.html` must link `output/output.css` (relative to the lecture folder), never `../output/...`.
- `node_modules/` and `output/` are git-ignored, so a fresh clone has no CSS until someone runs
  `npm install && npm run build`.

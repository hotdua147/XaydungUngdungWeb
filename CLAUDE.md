# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository purpose

Coursework monorepo for the "Xây dựng Ứng dụng Web" (Web App Development) course. It holds a sequence of
assignments that grows from plain HTML/CSS/JS exercises to a Vite + React midterm project. Assignment
content is written in Vietnamese; keep new content consistent with that.

## Structure

- `1-personal-tasks/<github-username>/` — individual student assignments, each a static `index.html` plus
  `css/style.css`. Four member folders exist on disk (`hotdua147`, `Cann2410`, `Ngocanh-22`,
  `nguyenchi2806`) but **only `1-personal-tasks/hotdua147/` is committed**; the others are untracked local
  work.
- `2-group-tasks/` — a shared static group project (plain HTML/CSS): the "E-commerce Front-end" team intro
  page. It links out to each member's personal page at `../1-personal-tasks/<username>/index.html`.
- `3-midterm-project/` — intended as a Vite + React project (`src/components`). On disk it currently has
  only `src/`, `public/`, and an installed `node_modules/`; there is **no `package.json` or `vite.config.js`**
  anywhere under the tracked tree, so npm scripts cannot be assumed to work. Treat it as work-in-progress.
- `.gitignore` — monorepo-style ignore rules: dependencies (`node_modules/`, package-manager stores), build
  outputs (`dist/`, `build/`, `out/`, `.next/`), logs, OS/IDE files, and secrets (`.env`, `.env.*`, with
  `.env.example` / `.env.template` kept). Do not commit anything these rules exclude.
- `.devcontainer/devcontainer.json` — image `mcr.microsoft.com/devcontainers/javascript-node:1-20-bullseye`;
  installs the Claude Code CLI in `postCreateCommand`, forwards port 5500 (Live Server default), and
  pre-installs the Live Server and Prettier VS Code extensions.

## Important structural quirk

`git ls-files` shows `XaydungUngdungWeb` registered as a **gitlink** (mode `160000`), but there is **no
`.gitmodules` file** and no nested `.git` directory inside it — a broken/orphaned submodule reference, not a
real submodule. On disk, `XaydungUngdungWeb/` holds an untracked, mostly duplicate copy of this repo's
structure (`1-personal-tasks/`, `2-group-tasks/`, `3-midterm-project/`), and that nested copy is the only
place an actual `package.json` and `vite.config.js` for the midterm project exist, alongside its own
`.devcontainer/` and `README.md`.

Do not assume anything under `XaydungUngdungWeb/` is tracked or in sync with the top-level folders of the
same name. Run `git status` / `git ls-files` before editing there, and prefer working in the top-level
folders unless a task specifically targets that nested tree.

## Working with this repo

- There is no build/lint/test tooling at the repo root — these are static HTML/CSS pages. Open the relevant
  `index.html` directly, or serve it with Live Server (the devcontainer forwards port 5500 for this).
- Before running npm commands in `3-midterm-project/`, confirm a `package.json` actually exists there; today
  it does not. The only committed Vite setup lives in the untracked `XaydungUngdungWeb/3-midterm-project/`.
- Put new personal assignments under `1-personal-tasks/<your-github-username>/` to match the per-student
  layout, and link them from `2-group-tasks/index.html` the same way existing members are linked.

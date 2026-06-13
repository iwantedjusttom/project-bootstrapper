---
name: project-bootstrapper
description: Kicks off a new Raeway Design build from a project brief. Use this skill whenever a new project is starting — when the user drops in a project brief, says "start a new app/project", "set up the workspace", "kick this off", or shares a client brief and wants the groundwork laid. It runs the first five steps of the build process — feature list, workspace setup, prototype, UI mockups, and design philosophy — so the user does not have to remember the sequence. Trigger it even if the user only says "new project" without naming the steps.
---

# Project Bootstrapper

This skill turns a project brief into a ready-to-build workspace by running five steps in order. The whole point is that Tom does not hold the process in his head — this file is the memory. Run the steps in sequence, write a status entry after each, and stop at the gates where his judgment is needed.

## Before you start

You need a project brief — a short doc (or message) describing what the app is, who it's for, and the business behind it. If there isn't one, ask for it before running. Find it in the project root (look for `BRIEF.md`, `PROJECT.md`, or a file the user points to). If the brief mentions a business, note its name, logo, and any brand colors — Step 1 and Step 4 use them.

Then create `PROGRESS.md` in the project root using the template in `references/progress-template.md`. Every step below ends by appending a status entry to it. This is how Tom sees where things are at a glance instead of digging through context.

## The five steps

### Step 1 — Feature list

Read the brief and extract a complete feature list. Each feature gets a short name, a one-line description, and a rough size (`S` / `M` / `L`). **Don't assign manual IDs** — this project runs on the GitHub-Issues pipeline, where **the issue number is the ID** (assigned in Step 2 when each feature becomes an issue). Don't tag "what code it touches" yet — that's guesswork before the architecture exists, and a stale map is worse than no map. Overlap gets handled by branch-per-feature off `main` and real merge conflicts during the build, not predicted upfront.

Hold the list as a working draft for now (don't write a tracking file) — it becomes the **GitHub Issues hopper** in Step 2, once the repo exists. Group features into phases if the brief implies a build order (Phase 1 = the thing that has to work first). Keep the list flat and scannable.

**Gate:** show Tom the feature list and the proposed phasing before moving on. This is the cheapest place to catch a missing or mis-scoped feature.

### Step 2 — Workspace setup

Set up the project hub using `references/workspace-template.md` as the model. This establishes the folder structure, the `CLAUDE.md` that becomes the project's persistent context (record that **work is tracked as GitHub Issues** via the design-queue → build-loop pipeline), the `PROGRESS.md` bootstrap log, and the git scaffolding. **There is no `FEATURES.md`** — the feature list becomes GitHub issues below. Initialize git and make the first commit once the structure is in place. Confirm the stack from the brief (default to Next.js + Supabase + Tailwind unless the brief says otherwise) and record it in `CLAUDE.md`.

**Put it on GitHub — this is a standard step, not an ad-hoc one.** Once the first commit exists, create the remote in the same move, so every project lands on GitHub the same way instead of being improvised later:

1. Confirm `gh` is ready: `gh auth status`. If it's not installed or not logged in, tell Tom to run `gh auth login` (one-time, browser) and pause here — don't fall back to a half-setup.
2. Make sure the default branch is `main` (`git branch -M main`).
3. Create the repo **private** and wire up the remote in one command, from the project root:
   ```
   gh repo create <project-name> --private --source=. --remote=origin --push
   ```
   Client work is private by default — never create a public repo unless Tom explicitly says so. Derive `<project-name>` from the project (match the folder/brand name); if it's ambiguous, ask rather than guess.
4. Confirm it worked: `gh repo view --web` should open the new private repo with the first commit pushed.

**Then set up the Issues hopper** — this is what replaces `FEATURES.md`:

5. Create the status labels: `gh label create ready` · `gh label create building` · `gh label create in-review` · `gh label create backlog` (`ready` = designed + build-ready; `building`/`in-review` = in flight; `backlog` = known but not yet designed).
6. **File the Step-1 feature list as GitHub issues** — one issue per feature (title = the feature name, body = the one-line description + size + phase). Label the genuinely build-ready foundation items `ready`; label everything still needing design/shaping `backlog` (design-queue promotes those to `ready` later with a mockup + spec). If the brief implies dated targets, create GitHub **Milestones** and assign issues.

Record the repo URL in `CLAUDE.md` so the project's permanent context knows where it lives. From here on, the **design-queue → build-loop** pipeline takes over (design-queue specs `backlog` → `ready`; build-loop builds `ready` → PR).

### Step 3 — Prototype

Build one working prototype of the app's core flow — the single most important thing the app does, end to end, even if rough. Not every feature. The prototype exists to make the thing real and surface design questions early. Mobile-first, always — that's non-negotiable on every Raeway build.

### Step 4 — UI mockups

Produce a few mockups of how key interactions could look — usually the screens where the user does the main work, plus one or two edge states (empty state, error). Pull the aesthetic from the business: logo, brand colors, the feel of their existing materials. If there's no brand to draw from, propose a direction and ask. Show real variation between mockups so there's an actual choice to make, not three versions of the same idea.

**Gate:** Tom picks a direction before the design philosophy gets locked. The mockups inform the philosophy doc, not the other way around.

### Step 5 — Design philosophy

Write `DESIGN.md` for the project, anchored on `references/design-philosophy.md` (the house style) but specialized to this app and the chosen mockup direction. This is what keeps the UI consistent as the build grows and as different agents touch it. It records: the color system, type choices, spacing/layout rules, component conventions, and the interaction principles for this specific app.

## After the five steps

Append a final `PROGRESS.md` entry summarizing what exists, then tell Tom what the next concrete build target is — point at **one `ready` issue**, not the whole hopper. The overwhelm comes from seeing everything at once; the antidote is naming the single next move (then design-queue/build-loop take it from there).

## A note on what this skill is NOT

It does not build the whole app. It lays the groundwork and stops. The ongoing build loop — developer work, review, QA — is a separate concern. Resist the urge to keep going past Step 5; the gates exist so Tom stays in control of direction.

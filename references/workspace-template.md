# Workspace Template — the Raeway project hub

The standard shape every new Raeway project starts in. The goal: drop into any project and instantly know where things live, with `CLAUDE.md` carrying the context so no agent (or future-you) starts blind.

## Folder structure

```
project-root/
├── CLAUDE.md          # persistent project context — the brain
├── BRIEF.md           # the original project brief
├── PROGRESS.md        # the bootstrap status log
├── DESIGN.md          # this project's design philosophy
├── /mockups           # UI mockups from Step 4 (+ design-queue specs)
├── /src               # the actual app
└── (standard stack scaffolding)
```

The **task list is GitHub Issues**, not a file in the repo — the design-queue → build-loop pipeline runs the hopper (labels `ready`/`building`/`in-review`/`backlog`) and Milestones for dated targets.

## CLAUDE.md contents

This is the file that makes a project resumable. It should contain, kept current:

- **What this is** — one paragraph: the app, who it's for, the business behind it.
- **Stack** — framework, DB, styling, deploy target. (Default: Next.js + Supabase + Tailwind, mobile-first, deployed on Vercel.)
- **Where things are** — the task hopper is **GitHub Issues** (read with `gh`); plus pointers to PROGRESS.md, DESIGN.md so any agent knows to read them.
- **Conventions** — anything non-obvious about how this codebase is organized.
- **Standing rules** — e.g. mobile-first is non-negotiable; RLS on every table; service role key never client-side.
- **Current focus** — mirrors PROGRESS.md's "next target" so context starts pointed at the right thing.

Keep CLAUDE.md tight. It's loaded into context constantly, so bloat costs tokens every session. Detailed history lives in PROGRESS.md, not here.

## Git setup

Initialize git, set up the remote, make the first commit after scaffolding. Default to branch-per-feature once the build starts — this is also the overlap-detector that lets parallel work stay safe.

## Stack defaults

Unless the brief says otherwise: Next.js + Supabase (auth, RLS, Storage, Realtime as needed) + Tailwind, mobile-first, Vercel deploy. Bake Supabase rate/security basics in from the start — RLS policies on every table, keep the service role key server-side only.

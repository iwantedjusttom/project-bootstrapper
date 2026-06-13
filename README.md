# project-bootstrapper

Kicks off a **new Raeway Design build** from a project brief.

Drop in a brief (or a client brief) and it runs the **first five steps** of the build process so you don't have to remember the sequence:

1. Feature list
2. Workspace setup
3. Prototype
4. UI mockups
5. Design philosophy

## Triggers

- a project brief dropped in
- "start a new app/project", "set up the workspace", "kick this off"
- sharing a client brief and wanting the groundwork laid
- even just "new project" without naming the steps

## Install

```powershell
git clone https://github.com/iwantedjusttom/project-bootstrapper.git
New-Item -ItemType Junction -Path "$HOME\.claude\skills\project-bootstrapper" -Target "<path>\project-bootstrapper"
```

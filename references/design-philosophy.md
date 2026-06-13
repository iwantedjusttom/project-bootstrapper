# Design Philosophy — Raeway house style

The default aesthetic and interaction principles that travel from project to project. Each project's own `DESIGN.md` starts here and specializes. **This is the file Tom should edit most heavily — it carries his taste, and these are starting defaults, not gospel.**

## Non-negotiables

- **Mobile-first, always.** Design the small screen first, then scale up. Every Raeway build assumes the primary user is on a phone unless proven otherwise.
- **Clean over clever.** If a screen needs explaining, it's too complex. Reduce until the obvious action is obvious.
- **One primary action per screen.** The user should never wonder what to do next.

## Visual language

- **Color from the business.** Pull the palette from the client's logo and brand. The app should feel like an extension of their identity, not a generic template. Pick one primary, one accent, and a neutral scale; resist adding more.
- **Type:** one display/heading face, one body face, max. Generous size and line-height on mobile — readability beats density.
- **Space is a feature.** Lean on whitespace and consistent spacing over borders and boxes to create structure.

## Interaction principles

- **States are not optional.** Every data view needs an empty state, a loading state, and an error state designed on purpose — not as afterthoughts. The empty state is often the most important screen a user sees.
- **Feedback is immediate.** Every tap acknowledges itself. No silent actions.
- **Forgiving by default.** Confirm destructive actions; make it easy to undo or back out.

## Component conventions

- Build a small, consistent set of components and reuse them. Consistency across screens reads as quality.
- Touch targets sized for thumbs, not cursors.

## How a project specializes this

A project's `DESIGN.md` keeps these principles but locks in the specifics: the actual hex values from the brand, the chosen type pairing, the spacing scale, and any app-specific interaction patterns that came out of the mockups. When agents build new screens later, they read `DESIGN.md` so the tenth screen looks like the first.

# AGENTS.md

## What this repo is

A library of style guides for AI agents. Agents read the guides before building UI in *other* projects and apply the tokens/rules there. This repo has no application code, no build, no tests, no CI — only markdown. Do not look for packages, scripts, or a dev server.

## Workflow contract (from README.md)

- When a user asks for a style, offer multiple style-guide choices and let them pick; then ask detailed requirements before implementing.
- Follow the chosen guide's restrictions and rules, combined with the target project's constraints.
- Only `styles/graphite.md` exists so far; each new style is a new `styles/*.md` file (e.g. `styles/aero.md`).

## Adding a new style guide

Use `styles/graphite.md` as the reference template. It is deliberately self-contained and project-agnostic — a guide must stand alone so an agent can implement it without reading anything else:

- Start with core principles, then a full token table, then concrete component/interaction/motion specs.
- Exact values everywhere: CSS custom properties (never raw hex in component CSS), px sizes, durations, easings.
- Ship both light (`:root`) and dark (`[data-theme="dark"]`) token sets.
- End with a conformance checklist an agent can verify before shipping.

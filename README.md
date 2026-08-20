# Agent Designer — Design Guide for AI Agents

[简体中文](README_CN.md)

Agent Designer is a repo of style guides for AI agents to read before they start designing. Each guide describes a coherent visual style with accurate descriptions and CSS tokens, so an agent can implement a good-looking appearance in any project.

## Usage

Agent Designer is meant to be read by an AI agent (such as opencode) before it starts designing UI in your project. Two common ways to use it:

### Use a style once

In a session with your agent, point it at a guide and ask for a style, e.g.:

> "Design my dashboard with the Graphite style from agent-designer (styles/graphite.md)."

The agent then:

1. Offers the available style choices (see Available styles).
2. Asks detailed requirements to reach the intended effect.
3. Follows the chosen guide's tokens and rules together with your project's constraints.
4. Verifies the result against the guide's conformance checklist before shipping.

### Make a style automatic for a project

To apply a style to every UI task in a project:

1. Generate the project's rules file with your agent — in opencode, run `/init` to create `AGENTS.md`.
2. Add a pointer to the guide, e.g.:

   `Before building any UI, read <path-to-agent-designer>/styles/graphite.md and apply its tokens and rules.`

3. The agent then applies the style by default on every UI task and checks conformance automatically.

## Workflow

- When a user wants the agent to pick a style to follow, the agent offers multiple style-guide choices and lets the user pick.
- Once selected, the agent asks detailed requirements to reach the intended effect.
- The agent follows the restrictions and requirements specified in the chosen style guide, combined with the project it is working on, to determine what style and widgets to use.

## Available styles

| Style | File | Description |
| --- | --- | --- |
| Graphite | `styles/graphite.md` | A general-purpose monochrome design system: gray-scale palette, sharp corners, 1px hairline borders, inverted hover states, uppercase micro-labels, paired light/dark themes. |

# Graphite — A General-Purpose Monochrome Design System

Graphite is a **monochrome, sharp-cornered, high-contrast** design system for
web interfaces. It is deliberately minimal: gray-scale palettes, 1px hairline
borders, uppercase micro-labels, and inverted hover states. It ships with a
paired light/dark theme that share the same structure, and it is easy for any
agent or team to apply to any project because everything is expressed as a
small set of tokens and rules.

This guide is self-contained and project-agnostic. Implement the tokens
exactly, follow the rules, and the result is consistent Graphite.

---

## 1. Core Principles

1. **Monochrome first.** Everything is gray-scale. Reserve accent color for
   transient feedback only (a success checkmark, a loading spinner) — and even
   those may reuse the foreground color.
2. **Sharp corners.** Nothing is rounded except affordances that are round by
   nature (spinners, radio dots, checkmark glyphs). Never add `border-radius`
   to boxes, buttons, badges, tooltips, inputs, or popovers.
3. **Hairline borders.** Separate surfaces with 1px borders, not shadows or
   elevation. No gradients, no blur, no 3D.
4. **Inverted hover.** The primary interactive cue is a full foreground /
   background inversion (dark ↔ light), mirrored in both themes.
5. **Micro-typography.** Uppercase, letter-spaced labels at 12–13px give the
   interface its instrument-panel character; body text stays quiet at 14px.
6. **Two themes, one layout.** Dark mode changes color only — never structure,
   spacing, or motion.
7. **Contained scrolling.** Content scrolls inside its container; controls
   never grow to fit content.

---

## 2. Color System

Colors are expressed as CSS custom properties on `:root` (light) and
overridden under `[data-theme="dark"]`. **Never use a raw hex in component
CSS — always reference a token.**

### Light tokens (default)

| Token                    | Value      | Role                                  |
| ------------------------ | ---------- | ------------------------------------- |
| `--bg-page`              | `#f9f9f9`  | Page / app background                 |
| `--surface`              | `#ffffff`  | Cards, panels, headers, inputs        |
| `--bg-subtle`            | `#f5f5f5`  | Badges, chips, quiet fills            |
| `--bg-subtle-hover`      | `#ececec`  | Hover for `--bg-subtle` fills         |
| `--border`               | `#e5e5e5`  | Hairline separators, input borders    |
| `--text-primary`         | `#111111`  | Headings, primary text, strong borders|
| `--text-secondary`       | `#666666`  | Labels, captions, meta text           |
| `--text-muted`           | `#999999`  | Placeholders, disabled hints, footers |
| `--inverse`              | `#111111`  | Inverted surface (tooltips, hover)    |
| `--on-inverse`           | `#ffffff`  | Text on `--inverse`                   |
| `--scrollbar-track`      | `#f5f5f5`  | Scrollbar track                       |
| `--scrollbar-thumb`      | `#d0d0d0`  | Scrollbar thumb                       |

### Dark tokens (`[data-theme="dark"]`)

| Token                | Value      |
| -------------------- | ---------- |
| `--bg-page`          | `#1c1c1e`  |
| `--surface`          | `#26262a`  |
| `--bg-subtle`        | `#3a3a3e`  |
| `--bg-subtle-hover`  | `#4a4a50`  |
| `--border`           | `#3f3f45`  |
| `--text-primary`     | `#e8e8ea`  |
| `--text-secondary`   | `#a2a2a8`  |
| `--text-muted`       | `#6e6e73`  |
| `--inverse`          | `#e8e8ea`  |
| `--on-inverse`       | `#111111`  |
| `--scrollbar-track`  | `#26262a`  |
| `--scrollbar-thumb`  | `#55555b`  |

### Rules

- Stay on the gray ramp. If you must add a semantic accent (success, danger),
  derive it from `--text-primary` / `--inverse` or use a single desaturated
  hue in BOTH themes with the same lightness relationship.
- Every light token has a dark counterpart; never introduce a color that has
  no dark-mode value.

---

## 3. Typography

| Role                | Family / Weight                  | Size | Tracking | Notes                    |
| ------------------- | -------------------------------- | ---- | -------- | ------------------------ |
| Body / default      | system stack, 400                | 14px | —        | Base size; line-height 1.5 |
| Display / title     | system stack, 600                | 20–28px | -0.5px | Page and section titles  |
| Micro label         | system stack, 600, **UPPERCASE** | 12px | 0.5px    | Panel/group headers      |
| Tiny label          | system stack, 600, UPPERCASE     | 10px | 1px      | Button micro-labels      |
| Meta / count        | system stack                     | 11px | —        | Counters, hints          |
| Monospace value     | `Monaco`, `Courier New`, monospace, 600 | 13px | — | Code-ish values (IDs, names) |
| Tooltip / popover   | system stack                     | 13px | 0.5px    | Small floating text      |

- Font stack: `-apple-system, BlinkMacSystemFont, 'Segoe UI', 'Arial', sans-serif`.
- Line heights: 1.5 general, 1.6 for long-form/text areas, 1.1 for tiny meta.
- Uppercase + tracking is the **label** language; never uppercase body copy.

---

## 4. Shape, Borders, Elevation

- **Corner radius:** `0` everywhere. (Round only circular primitives.)
- **Borders:** `1px solid var(--border)` for structure; `1px solid
  var(--text-primary)` for strong/primary button borders.
- **Elevation:** none. No `box-shadow`, no gradients. Layering is achieved by
  surface color and hairlines; floating elements (tooltips, popovers) use
  `--inverse` surface and high `z-index`.
- **Sizing rhythm:** 4px base unit. Use multiples: 4, 8, 12, 16, 24, 32.

---

## 5. Spacing

- Page gutters: 32px desktop, 16px tablet, 12px phone.
- Component padding: 8–16px.
- Gaps between grouped controls: 8–12px.
- Text container padding: 16px.
- Icon buttons: minimum 36×36px touch target.

---

## 6. Icons

- Inline SVG, 24×24 viewBox rendered at 18px (or 20px in headers).
- Stroke style: `stroke-width: 1.8`, `stroke-linecap: round`,
  `stroke-linejoin: round`, `fill: none`, `stroke: currentColor`.
- Color always inherits text color so icons adapt to hover inversion and dark
  mode automatically. Never hard-code icon colors.
- Keep icons inside the 18px box with clear padding; prefer simple, geometric
  shapes (circles, strokes, sparks) over detailed fills.

---

## 7. Components

### Header / top bar
- Full-width surface with a hairline bottom border; title left, actions right,
  `space-between`.
- Title: display size (24px/600/-0.5px). Action controls group with 8px gaps.

### Badge / chip
- `--bg-subtle` fill, 1px `--border`, 13px text, padding 8px 16px.
- Hover warms to `--bg-subtle-hover`. Optional chevron rotates 180° when open.

### Buttons
- **Base:** transparent fill, `1px solid var(--text-primary)` border, 14px/500,
  padding 10px 16px, inline-flex with 8px gap.
- **Hover:** invert (`var(--inverse)` fill, `var(--on-inverse)` text).
- **Active:** opacity 0.8. **Disabled:** opacity 0.5, `not-allowed`, and no
  hover/active treatment.
- **Icon button:** padding 8px 10px, min 36×36px, icon-only.
- **Micro-label buttons:** icon + 10px uppercase label with 1px tracking.

### Tooltip / popover / bubble
- `--inverse` fill, `--on-inverse` text, square corners, 13px + 0.5px tracking.
- Anchored to its trigger with an 8px gap; arrow: a 6px CSS triangle pointing
  at the trigger. Appear/disappear via opacity transition only.

### Panels / cards
- 1px `--border`, `--surface` fill, column flex, `min-height: 0`.
- Panel header: hairline bottom border; uppercase micro label left, actions
  right. Header action buttons stretch full height and separate with a
  `border-left` hairline (no gap between them).

### Forms
- Inputs: 1px `--border`, `--surface` fill, 13px text, 8px 12px padding.
- Focus: border-color becomes `--text-primary`. Placeholder: `--text-muted`.
- Text areas: borderless inside panels, 14px/1.6, internal scrolling.

### Footer
- Hairline top border, `--surface`, muted 14px text; links darken and
  underline on hover. Meta text may be hidden on compact screens.

### Scrollbars
- Custom WebKit scrollbars, 8px, square thumbs (`border-radius: 0`), track and
  thumb from tokens.

---

## 8. Interaction States

| State    | Treatment                                              |
| -------- | ------------------------------------------------------ |
| Rest     | Token colors, no decoration                            |
| Hover    | Invert (buttons) or subtle-fill hover (badges, links: darken + underline) |
| Active   | Dim to 80% opacity                                     |
| Focus    | `--text-primary` border / outline on inputs            |
| Disabled | 50% opacity, `not-allowed`, suppress hover/active      |
| Success  | Swap icon for a `✓` (0.3s scale pulse); stale content fades to 35% |
| Loading  | Swap icon for a border spinner (14px, 2px, `currentColor`), 0.8s linear spin |

---

## 9. Motion

| Use case            | Property                | Easing    | Duration |
| ------------------- | ----------------------- | --------- | -------- |
| Buttons, generic    | all                     | ease-out  | 0.15s    |
| Chevron / arrow     | transform               | ease-out  | 0.2s     |
| Tooltip / bubble    | opacity                 | ease-out  | 0.2s     |
| Collapsible panels  | height + border         | ease      | 0.3s     |
| Success checkmark   | scale pulse             | ease-out  | 0.3s     |
| Spinner             | rotate, linear infinite | linear    | 0.8s     |

Motion is functional and restrained. No bounce, no spring, no choreography.

---

## 10. Dark Mode Implementation

Apply the theme via the `<html>` element attribute, and keep it in sync with a
`data-theme` selector:

```css
:root {
    /* light tokens (§2) */
}
[data-theme="dark"] {
    /* dark tokens (§2) */
    color-scheme: dark;
}
```

```js
// Apply once early (before first paint) to avoid a light-mode flash
document.documentElement.setAttribute('data-theme', 'dark');
```

- Theme choice lives in one place (e.g., `localStorage`); a first-visit
  default may be derived from time-of-day or `prefers-color-scheme`.
- Because all component CSS uses tokens, dark mode is automatic — never write
  theme-specific component rules.
- Set `color-scheme: dark` in dark mode so native form controls and scrollbars
  match.

---

## 11. Responsive Behavior

- **Tablet (≤1024px):** stack multi-column grids into a single column with
  `minmax(0, 1fr)` rows; headers wrap; full-width actions.
- **Phone (≤640px):** shrink gutters to 12px; stack bars; stretch buttons;
  hide secondary meta text.
- Scrolling is always internal to content containers; the page never grows
  past the viewport (use `flex: 1` + `min-height: 0` on the main area).

---

## 12. Conformance Checklist (for agents)

Before shipping any UI work:

- [ ] All colors reference tokens from §2 — no raw hex, no new hues.
- [ ] Every light-mode rule has a dark-mode counterpart (or uses tokens, which
      handle both).
- [ ] No `border-radius` on boxes, buttons, badges, inputs, or bubbles.
- [ ] Separators are 1px hairlines; no shadows, gradients, or elevation.
- [ ] Labels use uppercase + letter-spacing micro style; body text is 14px.
- [ ] Icons are stroke SVGs (1.8 width, round caps/joins, `currentColor`).
- [ ] Hover inverts or uses subtle-fill hover; disabled suppresses hover;
      success/loading swap the icon.
- [ ] Long text scrolls inside its container; nothing grows to fit content.
- [ ] Dark mode mirrors light mode in structure, spacing, and motion.
- [ ] Motion uses the durations/easings in §9.

---

*Graphite — monochrome, sharp, high-contrast. Keep it gray, keep it square,
keep it flat.*

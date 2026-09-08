# CLAUDE.md

Guidance for Claude Code (and any other contributor, human or AI) working in this repository.

## Stack & Conventions

**Hard constraints — do not violate these:**

1. **Single-file project.** The entire project must live in one `index.html` file, with all CSS and JavaScript inlined via `<style>` and `<script>` tags — never in separate `.css` or `.js` files, and never split across multiple HTML pages. Linking external images and external CSS/JavaScript libraries (e.g. via CDN `<link>`/`<script src>` tags) is allowed. No additional pages. This constraint exists so the finished project can be copy-pasted as a single file for sharing in class and on single-file code platforms.
2. **Vanilla only.** Use plain HTML, CSS, and JavaScript only — no frameworks or libraries that require a build step (no React, Vue, TypeScript, JSX, Sass, etc.), and no build tooling of any kind (no bundlers, transpilers, package.json scripts, etc.). Externally linked libraries loaded directly via `<script src>`/`<link>` in `index.html` are fine as long as they need no build step.

When making changes, keep everything inside `index.html` and avoid introducing any second HTML file, separate asset file, or build process.

## Tech stack (hard constraints — do not deviate)
- Vanilla HTML, CSS, and JavaScript only. No React, Vue, or any JS framework.
- Tailwind CSS for all styling (via CDN only).
- No backend, no database. Fully static site.
- A toggle for light and dark theme, with the choice remembered
  across visits.

## Working conventions
- Before implementing any non-trivial feature, ask clarifying
  questions about scope, edge cases, and constraints first —
  don't propose a plan until you've asked.

## Feature Plan

A portal where visitors browse and try a growing collection of small
web tools/learning artifacts, all inside the single `index.html`.
Mark a phase's checkbox done once it ships; once done, feel free to
prune that phase's detail down to a one-line summary to keep this
section skimmable.

### Data model
```js
const TOOLS = [
  { id: 'unit-converter', title: 'Unit Converter', description: '...', icon: '📐' },
  { id: 'color-palette', title: 'Color Palette Generator', description: '...', icon: '🎨' }
];
```
Adding a future tool = one `TOOLS` entry + one `<section id="view-<id>" hidden>`
+ that tool's own init function. The grid, router, and nav read from
`TOOLS` and never need to change.

### Key flows
- **Routing:** hash-based (`#/` = home, `#/<tool-id>` = that tool). Router
  runs on load and on `hashchange`; unrecognized/empty hash falls back to
  home. Refreshing on a tool's hash lands directly on that tool.
- **Theme:** `dark` class on `<html>`, persisted to `localStorage.theme`,
  restored by an inline pre-Tailwind `<script>` in `<head>` before first
  paint (no flash). Toggle button lives in the header, visible on every view.
- **Growth pattern:** see Data model above — this is what phase 1 exists to prove.

### Phase 1 — Portal shell + first 2 tools
- [ ] Status: not started
- Home view: grid of tool cards rendered from `TOOLS` (no "coming soon"
  placeholder — just the 2 real cards).
- Tool 1, Unit Converter: categories Length/Weight/Temperature; two
  synced value+unit fields, editable in either direction.
- Tool 2, Color Palette Generator: `<input type="color">` synced with a
  hex text input; generates ~7 shades via HSL lightness steps; click a
  swatch to copy its hex (Clipboard API + visual/live-region confirmation).
- Accessibility baseline: label/for on all inputs, one shared
  `aria-live` region for copy confirmations, focus moves to the new
  view's heading on route change.

### Phase 2+ — Additional tools (not yet scoped)
- No tools chosen yet. When starting a new one, follow the Data model
  pattern above; ask clarifying questions per Working conventions before
  planning it in detail.

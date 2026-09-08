# CLAUDE.md

Guidance for Claude Code (and any other contributor, human or AI) working in this repository.

## Stack & Conventions

**Hard constraints — do not violate these:**

1. **Single-file project.** The entire project must live in one `index.html` file, with all CSS and JavaScript inlined via `<style>` and `<script>` tags — never in separate `.css` or `.js` files, and never split across multiple HTML pages. Linking external images and external CSS/JavaScript libraries (e.g. via CDN `<link>`/`<script src>` tags) is allowed. No additional pages. This constraint exists so the finished project can be copy-pasted as a single file for sharing in class and on single-file code platforms.
2. **Vanilla only.** Use plain HTML, CSS, and JavaScript only — no frameworks or libraries that require a build step (no React, Vue, TypeScript, JSX, Sass, etc.), and no build tooling of any kind (no bundlers, transpilers, package.json scripts, etc.). Externally linked libraries loaded directly via `<script src>`/`<link>` in `index.html` are fine as long as they need no build step.

When making changes, keep everything inside `index.html` and avoid introducing any second HTML file, separate asset file, or build process.

# CLAUDE.md

## Project Overview

This repository demonstrates how to integrate [diagrams.net](https://www.diagrams.net) (draw.io) with GitHub. It provides tools for editing, storing, and version-controlling diagrams directly in GitHub repositories.

This is a static site served via GitHub Pages from the `main` branch.

## Repository Structure

- **`edit-diagram.html`** — Standalone page that edits diagrams stored in GitHub. Uses the GitHub Contents API for reading/writing files and embeds diagrams.net via iframe using its embed protocol (`postMessage` JSON messages).
- **`nanocms.js`** — JavaScript library for self-editing pages. Adds double-click-to-edit behavior for elements with class `nanocms-diagram`. In edit mode (`?action=edit`), provides Save/Cancel buttons and commits changes back to GitHub via the Contents API.
- **`nanocms.css`** — Styles for `nanocms-diagram` elements (responsive sizing) and a decorative shadow effect (`nanocms-shadow1`).
- **`self-editing.html`** — Example HTML page using Bootstrap with multiple embedded diagrams (PNG and inline SVG). Uses `nanocms.js` for editing. Contains large base64-encoded diagram data inline.
- **`self-editing.svg`** — SVG file with embedded PNG and JavaScript for self-editing capability.
- **`diagram.png`** — Example PNG diagram with embedded draw.io XML.
- **`diagram-light-dark.svg`** — Example SVG with CSS `prefers-color-scheme` dark mode.
- **`diagram-target-dark.svg`** — Example SVG with CSS `:target` dark mode (activated via `#dark` fragment).

## Key Technical Details

### diagrams.net Embed Protocol

The editor communicates with the host page via `postMessage`. Key message types:

- **`init`** — Editor is ready; host sends diagram data via `load` action
- **`save`** — User clicked save; host may request export for PNG/SVG/HTML formats
- **`export`** — Export complete; host receives the data (base64-encoded)
- **`exit`** — User closed the editor

### GitHub API Usage

Files are read/written via the GitHub Contents API (`https://api.github.com/repos/{owner}/{repo}/contents/{path}`). Authentication uses HTTP Basic Auth (username + password/token). The file's `sha` is required for updates to prevent conflicts.

### File Format Conventions

- PNG files use `xmlpng` format (PNG with embedded XML metadata)
- SVG files use `xmlsvg` format (SVG with embedded XML)
- HTML files use the `html` export format
- XML files are stored as plain draw.io XML

### Dark Mode

SVG dark mode uses CSS filters (`invert` + `hue-rotate`) applied either automatically via `@media (prefers-color-scheme: dark)` or manually via the `:target` pseudo-class with a `#dark` URL fragment. See `DARK-MODE.md`.

## Development Notes

- The default branch is `main`. The `edit-diagram.html` defaults `ref` to `main`.
- `self-editing.html` and `self-editing.svg` contain large base64-encoded data — edit these via the draw.io editor, not by hand.
- `nanocms.js` derives the repository org/name from `window.location` (hostname for org, first path segment for repo). This assumes GitHub Pages URL structure.
- No build step — all files are served as-is via GitHub Pages.
- No dependencies to install — pure vanilla JavaScript, HTML, and CSS.

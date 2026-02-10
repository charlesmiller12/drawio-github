# draw.io GitHub Integration

Tools and examples for using [diagrams.net](https://www.diagrams.net) (formerly draw.io) with GitHub. Edit, store, and version-control diagrams directly in your repositories.

For a high-level introduction, see the [draw.io Integration](https://github.com/jgraph/drawio-integration) documentation.

## Getting Started

The simplest way to use draw.io with GitHub is the built-in GitHub mode:

**[Open diagrams.net with GitHub mode](https://app.diagrams.net/?mode=github)**

This lets you open, edit, and save `.drawio`, `.png`, `.svg`, and `.xml` diagram files directly from your GitHub repositories.

For embedding diagrams in GitHub wikis, see [Embed Diagrams](https://github.com/jgraph/drawio/wiki/Embed-Diagrams).

## Supported File Formats

| Format | Description |
|--------|-------------|
| `.xml` | Default draw.io XML format |
| `.png` | PNG with embedded XML (editable image) |
| `.svg` | SVG with embedded XML (editable vector image) |
| `.html` | HTML wrapper with embedded diagram |

## Examples

### Diagram Editor for GitHub

![Diagram](https://jgraph.github.io/drawio-github/diagram.png)

[Edit](https://jgraph.github.io/drawio-github/edit-diagram.html?repo=drawio-github&path=diagram.png) |
[Edit As New](https://app.diagrams.net/#Uhttps%3A%2F%2Fraw.githubusercontent.com%2Fjgraph%2Fdrawio-github%2Fmain%2Fdiagram.png) |
[Edit with draw.io](https://app.diagrams.net/#Hjgraph%2Fdrawio-github%2Fmain%2Fdiagram.png)

[`edit-diagram.html`](https://jgraph.github.io/drawio-github/edit-diagram.html) provides a simple UI for editing diagrams stored in GitHub. It uses the GitHub Contents API for file I/O and embeds diagrams.net as an editor.

**URL parameters:**

| Parameter | Description |
|-----------|-------------|
| `user` | GitHub username |
| `pass` | GitHub password or personal access token |
| `org` | GitHub organization or username |
| `repo` | Repository name |
| `path` | File path within the repository |
| `ref` | Branch or tag (default: `main`) |
| `action=open` | Immediately open the diagram for editing |

### Self-Editing SVG

![Self-editing Diagram](https://jgraph.github.io/drawio-github/self-editing.svg)

[`self-editing.svg`](https://jgraph.github.io/drawio-github/self-editing.svg) is an SVG file with embedded PNG data. It works as a regular image (for `<img>` tags) but also supports in-place editing via JavaScript when opened directly. Click the link (not the image) to enable editing.

### Self-Editing HTML

[`self-editing.html`](https://jgraph.github.io/drawio-github/self-editing.html) is an HTML page with multiple embedded diagrams. It uses [`nanocms.js`](nanocms.js) for GitHub I/O and diagram editing, with Bootstrap for styling. Append `?action=edit` to the URL to enable editing and saving back to GitHub.

## Dark Mode

SVG diagrams can adapt to light/dark themes using CSS. See [Dark Mode documentation](DARK-MODE.md) for details on:

- Automatic dark mode via `prefers-color-scheme` media query
- Manual dark mode via CSS `:target` pseudo-class

| Light | Dark (system) | Dark (manual) |
|-------|---------------|---------------|
| ![Light](diagram-light-dark.svg) | ![System dark](diagram-light-dark.svg) | ![Manual dark](diagram-target-dark.svg#dark) |

## Project Structure

```
├── edit-diagram.html        # Standalone diagram editor with GitHub integration
├── self-editing.svg         # SVG with embedded editing capability
├── self-editing.html        # HTML page with multiple editable diagrams
├── nanocms.js               # JavaScript library for GitHub I/O and diagram editing
├── nanocms.css              # Styles for embedded diagrams
├── diagram.png              # Example PNG diagram
├── diagram-light-dark.svg   # Example SVG with system dark mode
├── diagram-target-dark.svg  # Example SVG with target-based dark mode
├── DARK-MODE.md             # Dark mode documentation
└── CLAUDE.md                # Development guidelines
```

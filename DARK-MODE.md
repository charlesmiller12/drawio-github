# Dark Mode for SVG Diagrams

## CSS color-scheme

In v26.0.0 and later, the ``light-dark()`` color function is used in SVG with ``color-scheme: light dark`` in the style. This will use the color scheme of the containing system, page or tag, eg. ``<img src="img.svg" style="color-scheme: dark;">``.

<a href="https://raw.githubusercontent.com/jgraph/drawio-github/master/diagram-new-light-dark.svg" target="_blank">Here</a> is an example of the new SVG format that will render in dark mode in GitHub markdown depending on your system setting:

![Diagram with new system dark mode](diagram-new-light-dark.svg)

---

Information for SVG exported with versions prior to v26.0.0. below this line.

draw.io SVG diagrams can automatically adapt to dark mode using CSS. There are two approaches depending on how much control you need.

## Automatic: `prefers-color-scheme` Media Query

This approach adapts the SVG automatically based on the user's system-level dark mode setting. Add the following CSS to the SVG `<defs>` section:

```css
<style type="text/css">
@media (prefers-color-scheme: dark) {
    svg {
        filter: invert(93%) hue-rotate(180deg);
        background-color: transparent !important;
    }
    image {
        filter: invert(100%) hue-rotate(180deg) saturate(1.25);
    }
}
</style>
```

The filter values above are optimized for GitHub's dark theme. Adjust `invert()` and `hue-rotate()` values to match your page's color scheme.

**Example** (renders in dark mode if your system is set to dark):

![Diagram with system dark mode](diagram-light-dark.svg)

[View raw SVG](https://raw.githubusercontent.com/jgraph/drawio-github/main/diagram-light-dark.svg)

## Manual: CSS `:target` Pseudo-Class

For explicit control over dark mode, use the `:target` pseudo-class. This enables dark mode when the image URL includes a `#dark` fragment (or any value matching the SVG's `id` attribute).

Replace the media query with:

```css
<style type="text/css">
svg:target {
    filter: invert(93%) hue-rotate(180deg);
}
svg:target[style^="background-color: rgb(255, 255, 255);"] {
    background-color: transparent !important;
}
:target image {
    filter: invert(100%) hue-rotate(180deg) saturate(1.25);
}
</style>
```

Then toggle dark mode by appending `#dark` to the image source:

```markdown
<!-- Dark mode enabled -->
![Diagram](diagram-target-dark.svg#dark)

<!-- Light mode (no fragment) -->
![Diagram](diagram-target-dark.svg)
```

**Dark:**
![Diagram with target dark mode](diagram-target-dark.svg#dark)

**Light:**
![Diagram with target dark mode](diagram-target-dark.svg)

### Dynamic Toggle with JavaScript

To automatically enable dark mode for all draw.io SVGs when the page has a non-white background:

```js
if (getComputedStyle(document.body).backgroundColor !== 'rgba(0, 0, 0, 0)') {
    document.querySelectorAll('img[src$=".drawio.svg"]')
        .forEach(img => img.src += '#dark');
}
```

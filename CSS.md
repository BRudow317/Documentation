# CSS Documentation

## References

## Stylesheet Scope
### Global Stylesheet
A stylesheet that is imported once at the root of the application and affects all components.
### CSS Module
A stylesheet that is scoped to a specific component, preventing styles from leaking out or being affected by other stylesheets.


## Naming Conventions

### Pseudo-class
#### :root
The highest-level element in the document tree (usually <html>). Variables declared here are globally available



## CSS Variables

### Custom Properties
CSS Custom Property `--variable-name: value;` Often called a "CSS Variable." This is a custom storage unit you create to hold a value.
example: 
```css

:root {
    --my-pretty-color: #02fd4eff;
    --default-color: #ffffffff;
}
```

### Semantic Role variables
Semantic Abstraction means the style of naming variables what they do like --dark-grey or --card-border-color instead of what they are like --color-1 or --color-2.
example: 
```css
.storyTitle {
  /* You say: "Use the primary text color, whatever that happens to be right now" */
  color: var(--text-primary); 
```

```css
:root {
    --text-primary: var(--default-color);
}
  /* The browser checks the user's system settings (prefers-color-scheme). */
/* If Light Mode: It resolves */
var(--text-primary) -> --default-color
/* If Dark Mode: It resolves */
var(--text-primary) -> --my-pretty-color
}
```

### Default State
```css
/* Set the variables */
:root {
  /* CUSTOM VARIABLES (Primitives) */
  --color-charcoal: #121212; /* A specific dark hex code */
  --color-paper:    #ffffff; /* A specific light hex code */

  /* Set the defaults using */
  --page-background: var(--color-charcoal); 
  --text-color:      var(--color-paper);
}
```

## @Media Queries
`@Media` is a CSS at-rule used to apply styles based on specific conditions, such as screen size or user preferences.
CSS Browser rules check the system settings for many different properties. Some common examples are:
### The Core Media Features
#### Viewport & Layout (The Classics)
 - `prefers-color-scheme` (light or dark mode)
 - `width` (in px, em, rem, etc.)
 - `height` (in px, em, rem, etc.)
 - `min-height` (in px, em, rem, etc.)
 - `max-height` (in px, em, rem, etc.)
 - `min-width` (in px, em, rem, etc.)
 - `max-width` (in px, em, rem, etc.)
 - `aspect-ratio` (width/height)
 - `orientation` (landscape or portrait)
 - `resolution` (dpi or dppx)
#### Mobile Device Screens
 - `device-width` (in px, em, rem, etc.)
 - `device-height` (in px, em, rem, etc.)
 - `device-aspect-ratio` (width/height)
 - `size` (small, medium, large, x-large, xx-large)
#### Input Mechanism (Touch vs. Mouse)
 - `hover` (hover or none)
 - `pointer` (fine/mouse or coarse/touch or none)
 - `any-hover`/`any-pointer` (hover=mouse or none=touchscreen)
#### Other Accessibility & Options
 - `color` (number of bits per color component)
 - `monochrome` (number of bits per monochrome component)
 - `scrollbar-gutter` (auto, stable, or both-edges)
 - `prefers-reduced-motion` (reduce or no-preference)
 - `prefers-contrast` (high, low, or no-preference)
 - `inverted-colors` (inverted or none)
 - `scripting` (enabled or disabled)
 - `update` (fast or slow)

 - `resolution` (dpi or dppx)

 - `display-mode` (fullscreen, standalone, minimal-ui, or browser)
 - `light-level` (dim, normal, or washed)
 - `color-gamut` (srgb, p3, or rec2020)
 - `grid` (0, 1, or 2+)
 - `scan` (interlace or progressive)
 - `window-placement` (fullscreen, windowed, or minimized)
 - `overscan` (none or inset)
 - `dynamic-range` (standard or high)
 - `prefers-reduced-transparency` (reduce or no-preference)
 - `prefers-reduced-motion` (reduce or no-preference)
 - `window-segments` (single-fold-vertical, single-fold-horizontal, multi-fold-vertical, multi-fold-horizontal)
 - `forced-colors` (active or none)
 - `color-scheme` (normal, only light, or only dark)
 - `environment-blending` (opaque, additive, subtractive, or alpha-blend)
 - `backdrop-filter` (none or blur)

```css
@media (prefers-color-scheme: light) {
  /* ... overrides go here ... */
}
```
### prefers-color-scheme
An official system variable exposed by the User Agent (the browser) that reports the user's Operating System preference.
```css
@media (prefers-color-scheme: light) {
    :root {
      --page-background: var(--color-paper);
      --text-color:      var(--color-charcoal);
    }
}
```
### Multiple Condition queries
You can combine multiple conditions using logical operators like `and`, `or`, and `not`.
```css
@media (min-width: 768px) and (prefers-color-scheme: dark) {
  :root {
    --page-background: #1a1a1a;
    /* Font size bumps up for tablets in the dark */
    --base-font-size: 18px; 
  }
}
```
### The "NOT" Operator
Use the keyword not. It inverts the logic.
```css
@media not (hover: hover) {
  .tooltip {
    display: none; /* Don't show tooltips if they can't hover */
  }
}
```

### The "OR" Operator
Use a comma `,` to separate multiple conditions. It acts as a logical OR.
```css
@media (max-width: 600px), (prefers-reduced-motion: reduce) {
  .animated-element {
    animation: none; /* Disable animations on small screens or if user prefers reduced motion */
  }
}
```

### Comparison Operators
comparison operators (<, >, <=, >=) can be used in media queries to create more complex conditions.
```css
@media (width >= 800px) and (width <= 1200px) {
  .responsive-element {
    width: 80%; /* Apply styles for medium-sized screens */
  }
}
```
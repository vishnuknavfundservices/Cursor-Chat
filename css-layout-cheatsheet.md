# CSS Layout Cheatsheet 📐

## Quick Decision Guide

### When to Use Each Layout Method:

| Layout Method | Best For | Key Properties |
|--------------|----------|----------------|
| **Flexbox** | One-dimensional layouts, navigation bars, card layouts | `display: flex`, `justify-content`, `align-items` |
| **CSS Grid** | Two-dimensional layouts, complex page structures | `display: grid`, `grid-template-columns`, `grid-template-rows` |
| **Position** | Overlays, tooltips, fixed headers | `position: relative/absolute/fixed/sticky` |
| **Float** | Legacy layouts, text wrapping | `float: left/right`, `clear` |
| **Multi-column** | Text in newspaper style | `column-count`, `column-gap` |

## 1. Flexbox Quick Reference

### Container Properties:
```css
.flex-container {
    display: flex;
    
    /* Direction */
    flex-direction: row | row-reverse | column | column-reverse;
    
    /* Wrapping */
    flex-wrap: nowrap | wrap | wrap-reverse;
    
    /* Main axis alignment */
    justify-content: flex-start | flex-end | center | 
                    space-between | space-around | space-evenly;
    
    /* Cross axis alignment */
    align-items: stretch | flex-start | flex-end | center | baseline;
    
    /* Multiple lines alignment */
    align-content: flex-start | flex-end | center | 
                   space-between | space-around | stretch;
    
    /* Gap between items */
    gap: 20px;
}
```

### Item Properties:
```css
.flex-item {
    /* Growth factor */
    flex-grow: 0;
    
    /* Shrink factor */
    flex-shrink: 1;
    
    /* Base size */
    flex-basis: auto;
    
    /* Shorthand */
    flex: 1 1 auto;
    
    /* Individual alignment */
    align-self: auto | flex-start | flex-end | center | baseline | stretch;
    
    /* Order */
    order: 0;
}
```

## 2. CSS Grid Quick Reference

### Container Properties:
```css
.grid-container {
    display: grid;
    
    /* Define columns */
    grid-template-columns: 200px 1fr 200px;
    grid-template-columns: repeat(3, 1fr);
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    
    /* Define rows */
    grid-template-rows: 100px auto 100px;
    
    /* Named areas */
    grid-template-areas:
        "header header"
        "sidebar main"
        "footer footer";
    
    /* Gaps */
    gap: 20px;
    column-gap: 20px;
    row-gap: 10px;
    
    /* Auto sizing */
    grid-auto-columns: 200px;
    grid-auto-rows: minmax(100px, auto);
    
    /* Flow direction */
    grid-auto-flow: row | column | row dense | column dense;
}
```

### Item Properties:
```css
.grid-item {
    /* Placement by line numbers */
    grid-column: 1 / 3;
    grid-row: 2 / 4;
    
    /* Span syntax */
    grid-column: span 2;
    grid-row: span 3;
    
    /* Named area */
    grid-area: header;
    
    /* Alignment */
    justify-self: start | end | center | stretch;
    align-self: start | end | center | stretch;
}
```

## 3. Common Layout Patterns

### Center Everything
```css
.center {
    display: flex;
    justify-content: center;
    align-items: center;
    min-height: 100vh;
}

/* Or with Grid */
.center-grid {
    display: grid;
    place-items: center;
    min-height: 100vh;
}
```

### Sticky Footer
```css
.page {
    display: flex;
    flex-direction: column;
    min-height: 100vh;
}

.content {
    flex: 1;
}

.footer {
    flex-shrink: 0;
}
```

### Sidebar Layout
```css
.layout {
    display: grid;
    grid-template-columns: 250px 1fr;
    min-height: 100vh;
}

/* Or with Flexbox */
.layout-flex {
    display: flex;
}

.sidebar {
    flex: 0 0 250px;
}

.main {
    flex: 1;
}
```

### Responsive Cards
```css
.cards {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    gap: 20px;
}

/* Or with Flexbox */
.cards-flex {
    display: flex;
    flex-wrap: wrap;
    gap: 20px;
}

.card {
    flex: 1 1 300px;
}
```

### Holy Grail Layout
```css
.holy-grail {
    display: grid;
    grid-template-areas:
        "header header header"
        "nav main aside"
        "footer footer footer";
    grid-template-columns: 200px 1fr 200px;
    grid-template-rows: auto 1fr auto;
    min-height: 100vh;
}
```

## 4. Responsive Design

### Mobile-First Media Queries
```css
/* Base styles for mobile */
.container {
    padding: 1rem;
}

/* Tablet and up */
@media (min-width: 768px) {
    .container {
        max-width: 750px;
        margin: 0 auto;
    }
}

/* Desktop and up */
@media (min-width: 1024px) {
    .container {
        max-width: 1200px;
    }
}

/* Large screens */
@media (min-width: 1440px) {
    .container {
        max-width: 1400px;
    }
}
```

### Container Queries (Modern)
```css
.card-container {
    container-type: inline-size;
}

@container (min-width: 400px) {
    .card {
        display: flex;
        gap: 20px;
    }
}
```

## 5. Modern CSS Features

### Aspect Ratio
```css
.video {
    aspect-ratio: 16 / 9;
    width: 100%;
}
```

### Clamp (Fluid Typography)
```css
.title {
    font-size: clamp(1.5rem, 4vw, 3rem);
}
```

### Logical Properties
```css
.box {
    margin-inline: auto; /* left and right */
    padding-block: 2rem; /* top and bottom */
    border-inline-start: 3px solid; /* left in LTR */
}
```

### CSS Custom Properties for Layouts
```css
:root {
    --sidebar-width: 250px;
    --header-height: 60px;
    --gap: 20px;
}

.layout {
    display: grid;
    grid-template-columns: var(--sidebar-width) 1fr;
    gap: var(--gap);
    padding-top: var(--header-height);
}
```

## 6. Browser Support Tips

### Feature Detection
```css
/* Fallback for older browsers */
.container {
    display: block;
}

/* Modern browsers */
@supports (display: grid) {
    .container {
        display: grid;
        grid-template-columns: repeat(3, 1fr);
    }
}
```

### Vendor Prefixes (if needed)
```css
.flex {
    display: -webkit-box;
    display: -ms-flexbox;
    display: flex;
}
```

## 7. Performance Tips

1. **Use CSS Grid for 2D layouts** - More performant than nested flexbox
2. **Avoid deep nesting** - Keep selectors simple
3. **Use transform for animations** - Better performance than position changes
4. **Consider contain property** - For layout isolation
5. **Use will-change sparingly** - Only for elements that will animate

## 8. Debugging Tips

```css
/* Visual debugging */
* {
    outline: 1px solid red !important;
}

/* Grid debugging */
.grid {
    display: grid;
    /* Firefox/Chrome DevTools have built-in grid inspectors */
}

/* Flexbox debugging */
.flex {
    display: flex;
    /* Use browser DevTools flex inspector */
}
```

## Quick Decision Tree

```
Need to layout elements?
├── One direction (row OR column)?
│   └── Use Flexbox
├── Two dimensions (rows AND columns)?
│   └── Use CSS Grid
├── Overlap elements?
│   └── Use Position (absolute/fixed)
├── Text in columns?
│   └── Use Multi-column
└── Simple document flow?
    └── Use default block/inline
```

## Resources

- **Flexbox**: [CSS-Tricks Flexbox Guide](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)
- **Grid**: [CSS-Tricks Grid Guide](https://css-tricks.com/snippets/css/complete-guide-grid/)
- **Can I Use**: Check browser support for CSS features
- **MDN**: Comprehensive documentation for all CSS properties
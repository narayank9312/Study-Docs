### HTML/CSS Frequently Asked Questions

#### 1. Difference between (display: none, visibility: hidden, opacity: 0)
**Explanation:**
- `display: none`: Removes the element from the DOM flow, no space is allocated.
- `visibility: hidden`: Hides the element but retains the space in the DOM.
- `opacity: 0`: Makes the element invisible but still takes up space in the DOM and is interactable.

**Example:**
```html
<div style="display: none;">This is hidden</div>
<div style="visibility: hidden;">This is also hidden</div>
<div style="opacity: 0;">This is invisible</div>
```

#### 2. Ways to Hide Elements in DOM
**Explanation:**
- `display: none`
- `visibility: hidden`
- `opacity: 0`
- `position: absolute; left: -9999px;`
- `height: 0; width: 0; overflow: hidden;`

**Example:**
```html
<div style="display: none;">Hidden by display</div>
<div style="visibility: hidden;">Hidden by visibility</div>
<div style="opacity: 0;">Hidden by opacity</div>
<div style="position: absolute; left: -9999px;">Hidden by position</div>
<div style="height: 0; width: 0; overflow: hidden;">Hidden by size</div>
```

#### 3. Pseudo Class/ Pseudo Selector
**Explanation:** Pseudo-classes target elements based on their state, while pseudo-selectors target elements not explicitly mentioned in the DOM.

**Example:**
```css
a:hover {
    color: red;
}

p::before {
    content: "Prefix";
}
```

#### 4. What is a Box Model?
**Explanation:** The box model represents the structure of a web element, consisting of margins, borders, padding, and the content area.

**Example:**
```css
div {
    width: 100px;
    height: 100px;
    padding: 10px;
    border: 5px solid black;
    margin: 20px;
}
```

#### 5. Semantic Element vs Non-semantic Element
**Explanation:** Semantic elements (e.g., `<header>`, `<article>`) clearly describe their meaning, while non-semantic elements (e.g., `<div>`, `<span>`) do not.

**Example:**
```html
<header>This is a header</header>
<div>This could be anything</div>
```

#### 6. Layouts, Positioning, Responsive Design Techniques, CSS Preprocessors, Frameworks
**Explanation:**
- **Layouts:** Flexbox, Grid.
- **Positioning:** Static, relative, absolute, fixed, sticky.
- **Responsive Design:** Media queries, fluid grids.
- **CSS Preprocessors:** Sass, Less.
- **Frameworks:** Bootstrap, Material-UI.

**Example:**
```css
.container {
    display: flex;
    justify-content: center;
}

@media (max-width: 600px) {
    .container {
        flex-direction: column;
    }
}
```

#### 7. Web Accessibility
**Explanation:** Practices to ensure websites are usable by people with disabilities, e.g., using semantic HTML, ARIA roles.

**Example:**
```html
<button aria-label="Close">X</button>
```

#### 8. SEO
**Explanation:** Techniques to improve a website's visibility in search engines, e.g., meta tags, alt attributes.

**Example:**
```html
<meta name="description" content="This is an example website.">
<img src="image.jpg" alt="Example image">
```

#### 9. How Rendering Works (Reflow vs Repaint)
**Explanation:** 
- **Reflow:** Layout changes that affect the document's structure.
- **Repaint:** Visual changes that do not affect layout.

**Example:**
```css
/* Reflow */
div {
    width: 100px;
}

/* Repaint */
div {
    background-color: red;
}
```

#### 10. Centering a Div
**Explanation:** Multiple ways to center a div, both horizontally and vertically.

**Example:**
```css
/* Flexbox */
.parent {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
}

/* Grid */
.parent {
    display: grid;
    place-items: center;
    height: 100vh;
}

/* Margin Auto */
.child {
    width: 50%;
    margin: 0 auto;
}
```

#### 11. Async and Defer
**Explanation:** `async` and `defer` attributes for `<script>` tags manage loading and execution of scripts.

**Example:**
```html
<!-- Async: script loads and executes asynchronously -->
<script src="script.js" async></script>

<!-- Defer: script loads asynchronously and executes after HTML parsing -->
<script src="script.js" defer></script>
```

### Conclusion
These detailed explanations and examples provide a comprehensive understanding of common HTML/CSS interview topics, helping you prepare effectively. If you need further clarification or additional examples, feel free to ask!
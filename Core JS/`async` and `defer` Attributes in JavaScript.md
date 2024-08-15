### `async` and `defer` Attributes in JavaScript

**Concept**: Both `async` and `defer` are attributes that can be added to the `<script>` tag to control the loading behavior of external scripts in HTML.

### `async` Attribute

- **Behavior**: Loads the script asynchronously. The script is fetched in the background and executed as soon as it is available.
- **Use Case**: Suitable for independent scripts that don't rely on other scripts or the DOM being fully loaded.

**Example**:
```html
<script src="script.js" async></script>
```

### Flow Diagram for `async`:

1. **HTML Parsing**:
   - The browser starts parsing HTML.
2. **Async Script Loading**:
   - The script is fetched asynchronously.
3. **Script Execution**:
   - The script executes as soon as it is available, potentially before the HTML is fully parsed.

### `defer` Attribute

- **Behavior**: Loads the script asynchronously but ensures that it is executed only after the HTML is fully parsed.
- **Use Case**: Suitable for scripts that need the DOM to be fully constructed before execution.

**Example**:
```html
<script src="script.js" defer></script>
```

### Flow Diagram for `defer`:

1. **HTML Parsing**:
   - The browser starts parsing HTML.
2. **Defer Script Loading**:
   - The script is fetched asynchronously.
3. **HTML Parsing Complete**:
   - The script executes after the HTML is fully parsed.

### Summary:

- **`async`**: Fetches script asynchronously and executes it as soon as it's available.
- **`defer`**: Fetches script asynchronously and executes it after the HTML parsing is complete.

Both attributes help improve page load performance by allowing scripts to load without blocking HTML parsing. Choose `async` for independent scripts and `defer` for scripts that depend on the DOM being fully loaded.
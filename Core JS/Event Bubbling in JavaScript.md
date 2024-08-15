### Event Bubbling in JavaScript

**Concept**: Event bubbling is a method where an event starts from the deepest target element and propagates up to the parent elements.

### Example:

**HTML Structure**:
```html
<!DOCTYPE html>
<html>
<head>
  <title>Event Bubbling</title>
</head>
<body>
  <div id="parent">
    Parent
    <div id="child">
      Child
      <button id="button">Click me</button>
    </div>
  </div>
  <script src="script.js"></script>
</body>
</html>
```

**JavaScript** (`script.js`):
```javascript
document.getElementById('parent').addEventListener('click', function() {
  alert('Parent clicked');
});

document.getElementById('child').addEventListener('click', function() {
  alert('Child clicked');
});

document.getElementById('button').addEventListener('click', function() {
  alert('Button clicked');
});
```

### Flow Diagram:

1. **Click on Button**:
   - Event starts at `button`.
2. **Bubbles Up**:
   - Event propagates to `child`.
3. **Bubbles Further**:
   - Event propagates to `parent`.

### Visualization:

```
    [Parent (alert: "Parent clicked")]
         ↑
    [Child (alert: "Child clicked")]
         ↑
    [Button (alert: "Button clicked")]
```

### Explanation:

- When the button is clicked, the event first triggers the `button`'s event handler.
- Then it bubbles up to the `child`'s event handler.
- Finally, it bubbles up to the `parent`'s event handler.

Event bubbling allows multiple elements to respond to the same event, which can be useful for handling events in a more centralized way.
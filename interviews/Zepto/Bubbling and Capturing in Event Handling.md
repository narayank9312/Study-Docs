### Bubbling and Capturing in Event Handling

In web development, event handling in the DOM (Document Object Model) can occur in two phases: **event capturing** and **event bubbling**. These phases determine the order in which event handlers are invoked when an event occurs on an element within a nested hierarchy of elements.

### Event Bubbling

Event bubbling is the default behavior. When an event occurs on an element, it first triggers the event handlers on that element. The event then "bubbles up" to the parent elements, triggering their event handlers, and continues to bubble up until it reaches the document root.

### Event Capturing

Event capturing (also known as trickling) is the opposite of bubbling. The event starts from the document root and trickles down to the target element. This phase is less commonly used but can be useful in certain scenarios.

### Practical Use Cases

1. **Event Delegation**: Using event bubbling to handle events on dynamically added elements.
2. **Preventing Event Propagation**: Stopping the event from reaching parent elements.
3. **Capturing Phase for Early Intervention**: Using capturing to intercept events before they reach the target.

### Example Scenario: Event Delegation

#### HTML Structure

```html
<div id="parent">
  <button class="child">Button 1</button>
  <button class="child">Button 2</button>
  <button class="child">Button 3</button>
</div>
```

#### JavaScript for Event Delegation Using Bubbling

Instead of attaching event handlers to each button, you can attach a single event handler to the parent element. This handler will catch the event during the bubbling phase.

```javascript
document.getElementById('parent').addEventListener('click', function(event) {
  if (event.target && event.target.classList.contains('child')) {
    console.log(`Button ${event.target.textContent} clicked`);
  }
});
```

**Explanation**:
- The event listener is attached to the parent `<div>`.
- When any button is clicked, the event bubbles up to the parent.
- The parent’s event listener checks if the clicked element (`event.target`) has the class `child`.

#### JavaScript for Preventing Event Bubbling

```javascript
document.getElementById('parent').addEventListener('click', function(event) {
  if (event.target && event.target.classList.contains('child')) {
    console.log(`Button ${event.target.textContent} clicked`);
    event.stopPropagation(); // Prevents the event from bubbling up further
  }
});
```

**Explanation**:
- `event.stopPropagation()` stops the event from bubbling up to the parent elements.

### Example Scenario: Event Capturing

To use the capturing phase, you can pass a third argument (`true`) to `addEventListener`.

```javascript
document.getElementById('parent').addEventListener('click', function(event) {
  console.log('Parent capturing');
}, true);

document.querySelectorAll('.child').forEach(button => {
  button.addEventListener('click', function(event) {
    console.log(`Button ${this.textContent} capturing`);
  }, true);
});
```

**Explanation**:
- The parent and button event listeners are set to capture (`true`).
- The event is intercepted in the capturing phase before reaching the target.

### Complete Example

Here’s a complete example demonstrating both capturing and bubbling phases:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Event Bubbling and Capturing</title>
</head>
<body>
  <div id="parent">
    <button class="child">Button 1</button>
    <button class="child">Button 2</button>
    <button class="child">Button 3</button>
  </div>

  <script>
    // Event capturing phase
    document.getElementById('parent').addEventListener('click', function(event) {
      console.log('Parent capturing');
    }, true);

    document.querySelectorAll('.child').forEach(button => {
      button.addEventListener('click', function(event) {
        console.log(`Button ${this.textContent} capturing`);
      }, true);
    });

    // Event bubbling phase
    document.getElementById('parent').addEventListener('click', function(event) {
      console.log('Parent bubbling');
    });

    document.querySelectorAll('.child').forEach(button => {
      button.addEventListener('click', function(event) {
        console.log(`Button ${this.textContent} bubbling`);
      });
    });

    // Example of stopping propagation
    document.querySelector('.child').addEventListener('click', function(event) {
      console.log('Stopping propagation');
      event.stopPropagation();
    });
  </script>
</body>
</html>
```

### Explanation

- **Capturing Phase**:
  - Event listeners on the parent and buttons are set to capture (`true`).
  - These listeners log messages during the capturing phase.
  
- **Bubbling Phase**:
  - Event listeners on the parent and buttons handle the event during the bubbling phase.
  - The event logs messages as it bubbles up from the buttons to the parent.
  
- **Stopping Propagation**:
  - The first button's click event stops further propagation using `event.stopPropagation()`.

### Summary

- **Event Bubbling**: The event propagates from the target element up through its ancestors.
- **Event Capturing**: The event propagates from the document root down to the target element.
- **Use Cases**: Event delegation, stopping propagation, and using capturing for early event interception.

Understanding these concepts helps in managing events effectively in web applications.
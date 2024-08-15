### IIFE (Immediately Invoked Function Expression) in JavaScript

**Concept**:
An IIFE is a function that runs as soon as it is defined. It is often used to create a private scope to avoid polluting the global namespace.

### Syntax:

```javascript
(function() {
  // Code to be executed immediately
})();

// or with arrow functions (ES6)
(() => {
  // Code to be executed immediately
})();
```

### Example:

```javascript
(function() {
  const message = "Hello, World!";
  console.log(message); // Output: Hello, World!
})();

(() => {
  const number = 42;
  console.log(number); // Output: 42
})();
```

### Use Cases:
1. **Avoiding Global Variables**:
   - Encapsulate variables and functions to avoid conflicts in the global scope.
   
2. **Private Variables and Functions**:
   - Create private variables and functions that cannot be accessed from outside the IIFE.

### Explanation:
- The function is defined and immediately executed due to the parentheses `()` at the end.
- Helps to keep the global scope clean by creating a private scope.

By using IIFEs, you can manage variable scope and prevent conflicts, making your code cleaner and more modular.
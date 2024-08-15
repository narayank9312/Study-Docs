### Debouncing in JavaScript

**Concept**: Debouncing is a technique to limit the rate at which a function executes. It ensures that the function runs only once after a specified period of time has elapsed since the last time it was invoked.

### Example:

**Function**:
```javascript
function debounce(func, delay) {
  let debounceTimer;
  return function(...args) {
    const context = this;
    clearTimeout(debounceTimer);
    debounceTimer = setTimeout(() => func.apply(context, args), delay);
  };
}
```

**Usage**:
```javascript
const handleResize = debounce(() => {
  console.log('Window resized');
}, 500);

window.addEventListener('resize', handleResize);
```

### Flow Diagram:

1. **Event Triggered**:
   - User triggers an event (e.g., window resize).
2. **Clear Timer**:
   - Clear any existing timer.
3. **Set Timer**:
   - Set a new timer for the specified delay.
4. **Execute Function**:
   - Function executes only if no new event is triggered within the delay period.

### Practical Example:

**Search Input**:
```javascript
const searchInput = document.getElementById('search');

const handleSearch = debounce((event) => {
  console.log('Search query:', event.target.value);
}, 300);

searchInput.addEventListener('input', handleSearch);
```

**Explanation**:

- **Event Handling**: The function runs only after the user has stopped typing for 300 milliseconds.
- **Use Case**: Reduces the number of API calls in search input fields, improving performance and user experience.

By using debouncing, you can optimize performance and prevent unnecessary function calls, especially in scenarios like resizing windows, searching, and scrolling.
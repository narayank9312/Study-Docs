### Debouncing vs Throttling in JavaScript

**Debouncing**:
- **Concept**: Ensures that a function is only executed after a certain period of time has passed since it was last invoked.
- **Use Case**: Prevents multiple calls within a short time, e.g., resizing window, searching as you type.
- **Example**:
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

**Throttling**:
- **Concept**: Ensures that a function is only executed at most once in a specified period.
- **Use Case**: Limits the number of executions over time, e.g., scrolling, resizing events.
- **Example**:
  ```javascript
  function throttle(func, limit) {
    let lastFunc;
    let lastRan;
    return function(...args) {
      const context = this;
      if (!lastRan) {
        func.apply(context, args);
        lastRan = Date.now();
      } else {
        clearTimeout(lastFunc);
        lastFunc = setTimeout(function() {
          if (Date.now() - lastRan >= limit) {
            func.apply(context, args);
            lastRan = Date.now();
          }
        }, limit - (Date.now() - lastRan));
      }
    };
  }
  ```

### Summary:

- **Debouncing**: Executes the function after a specified delay if no new event occurs during that delay.
- **Throttling**: Ensures the function executes at most once in a specified period, regardless of how many times the event occurs.

Both techniques are useful for performance optimization, particularly in scenarios with frequent events.

### Debouncing vs Throttling: Use Cases and Practical Examples

**Debouncing**:

**Use Case**: Search Input
- **Scenario**: Updating search results as the user types.
- **Goal**: Minimize API calls by waiting until the user stops typing.

**Example**:
```javascript
function debounce(func, delay) {
  let debounceTimer;
  return function(...args) {
    const context = this;
    clearTimeout(debounceTimer);
    debounceTimer = setTimeout(() => func.apply(context, args), delay);
  };
}

const searchInput = document.getElementById('search');
const handleSearch = debounce((event) => {
  console.log('Fetching search results for:', event.target.value);
}, 300);

searchInput.addEventListener('input', handleSearch);
```

**Throttling**:

**Use Case**: Window Resize
- **Scenario**: Performing calculations when the window is resized.
- **Goal**: Limit the number of calculations during continuous resizing.

**Example**:
```javascript
function throttle(func, limit) {
  let lastFunc;
  let lastRan;
  return function(...args) {
    const context = this;
    if (!lastRan) {
      func.apply(context, args);
      lastRan = Date.now();
    } else {
      clearTimeout(lastFunc);
      lastFunc = setTimeout(function() {
        if (Date.now() - lastRan >= limit) {
          func.apply(context, args);
          lastRan = Date.now();
        }
      }, limit - (Date.now() - lastRan));
    }
  };
}

const handleResize = throttle(() => {
  console.log('Window resized:', window.innerWidth, window.innerHeight);
}, 1000);

window.addEventListener('resize', handleResize);
```

### Explanation:
- **Debouncing** delays execution until after the last event in a series of rapid events.
- **Throttling** limits execution to once every specified period.


### Throttling in JavaScript

**Concept**: Throttling is a technique that limits the number of times a function can be called over time. It ensures a function is called at most once every specified interval.

### Use Case: Window Resize Event
**Scenario**: Performing calculations when the window is resized to avoid excessive calls.

**Example**:
```javascript
function throttle(func, limit) {
  let lastFunc;
  let lastRan;
  return function(...args) {
    const context = this;
    if (!lastRan) {
      func.apply(context, args);
      lastRan = Date.now();
    } else {
      clearTimeout(lastFunc);
      lastFunc = setTimeout(function() {
        if (Date.now() - lastRan >= limit) {
          func.apply(context, args);
          lastRan = Date.now();
        }
      }, limit - (Date.now() - lastRan));
    }
  };
}

const handleResize = throttle(() => {
  console.log('Window resized:', window.innerWidth, window.innerHeight);
}, 1000);

window.addEventListener('resize', handleResize);
```

### Explanation:
- **Throttle Function**: Limits the `handleResize` function to be called once every 1000 milliseconds (1 second), ensuring efficient execution during continuous resizing events.

Throttling is particularly useful for performance optimization in scenarios involving frequent events like scrolling, resizing, or mouse movements.
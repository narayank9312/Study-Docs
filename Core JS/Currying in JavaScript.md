### Currying in JavaScript

**Concept**: Currying is the process of transforming a function that takes multiple arguments into a sequence of functions that each take a single argument.

### Example:

**Uncurried Function**:
```javascript
function add(a, b) {
  return a + b;
}
console.log(add(2, 3)); // 5
```

**Curried Function**:
```javascript
function curryAdd(a) {
  return function(b) {
    return a + b;
  };
}

const addTwo = curryAdd(2);
console.log(addTwo(3)); // 5

// Or more directly:
console.log(curryAdd(2)(3)); // 5
```

### Flow Diagram:

```
    curryAdd(2)         -> returns function(b) { return 2 + b; }
          ↓
     function(b)
          ↓
  b = 3, returns 2 + 3 -> 5
```

### Practical Example:
**Using Currying for Configurable Functions**:
```javascript
function multiply(a) {
  return function(b) {
    return a * b;
  };
}

const double = multiply(2);
console.log(double(5)); // 10

const triple = multiply(3);
console.log(triple(5)); // 15
```

### Explanation:
- **Step 1**: `curryAdd(2)` returns a new function `function(b) { return 2 + b; }`.
- **Step 2**: The returned function is called with the argument `3`.
- **Step 3**: The result is `2 + 3`, which is `5`.

Currying is useful for creating reusable and configurable functions by pre-setting some of the arguments.

### Currying with Closures in JavaScript

Currying can be achieved using closures. Closures allow a function to access variables from an outer function even after the outer function has returned.

### Example:

**Curried Function using Closures**:
```javascript
function curryAdd(a) {
  return function(b) {
    return a + b;
  };
}

// Using the curried function
const addTwo = curryAdd(2);
console.log(addTwo(3)); // 5

// Or more directly
console.log(curryAdd(2)(3)); // 5
```

### Flow Diagram:

1. **Call `curryAdd(2)`**:
   - `curryAdd` returns a new function `function(b) { return a + b; }`
   - The value `a` is set to `2` and remembered by the closure.
   ```
   curryAdd(2) -> returns function(b) { return 2 + b; }
   ```

2. **Call the returned function with `3`**:
   - The function uses the remembered value of `a` and computes `2 + 3`
   ```
   function(b)
        ↓
   b = 3, returns 2 + 3 -> 5
   ```

### Practical Example with Multiple Arguments:

**Multiplication Example**:
```javascript
function multiply(a) {
  return function(b) {
    return a * b;
  };
}

// Creating a partially applied function
const double = multiply(2);
console.log(double(5)); // 10

const triple = multiply(3);
console.log(triple(5)); // 15
```

### Explanation:

1. **`curryAdd(2)`**:
   - Returns a new function that takes `b` and returns `a + b`.
   - `a` is set to `2` and remembered by the returned function.

2. **Calling the returned function**:
   - Pass `3` to the returned function.
   - The function calculates `2 + 3`, using the value of `a` from the closure.

Using closures for currying allows you to create functions with preset parameters, which can be reused with different arguments. This technique is particularly useful for creating more modular and reusable code.
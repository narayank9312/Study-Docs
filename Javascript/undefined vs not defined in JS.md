### Summary of "undefined vs not defined in JS | Namaste JavaScript Ep. 6"

#### Key Points:

1. **Undefined**:
   - A variable is declared but not initialized.
   - Example:
     ```javascript
     let a;
     console.log(a); // Output: undefined
     ```

2. **Not Defined**:
   - A variable is not declared in the scope.
   - Example:
     ```javascript
     console.log(b); // Output: ReferenceError: b is not defined
     ```

3. **Usage in Functions**:
   - Parameters not passed to functions are `undefined`.

4. **Hoisting**:
   - Variables declared with `var` are hoisted and initialized to `undefined`.

#### Code Examples:

**Example 1: Undefined Variable**:
```javascript
let x;
console.log(x); // Output: undefined
x = 10;
console.log(x); // Output: 10
```

**Example 2: Not Defined Variable**:
```javascript
console.log(y); // Output: ReferenceError: y is not defined
let y = 20;
```

### Detailed Flowchart:

**1. Variable Initialization and Hoisting**:

```plaintext
During Compilation:
+-------------------+
| Global Context    |
|-------------------|
| var a;            |
| let b;            |
+-------------------+

During Execution:
+-------------------+
| Global Context    |
|-------------------|
| a = undefined;    |
| b = ReferenceError|
+-------------------+
```

For more details, watch the video [here](https://www.youtube.com/watch?v=B7iF6G3EyIk).
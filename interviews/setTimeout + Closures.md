
### Summary of "setTimeout + Closures Interview Question 🔥 | Namaste 🙏 JavaScript Ep. 11"

#### Key Points:

1. **setTimeout and Closures**:
   - Demonstrates how closures work with `setTimeout`.
   - Explains common pitfalls and interview questions related to closures and `setTimeout`.

2. **Common Pitfall**:
   - Loop variable in `setTimeout` callback often causes unexpected results due to closure capturing the same variable.

#### Code Examples:

**Example 1: Common Pitfall**:
```javascript
for (var i = 1; i <= 5; i++) {
  setTimeout(function() {
    console.log(i);
  }, i * 1000);
}
// Output: 6 (five times, after each second)
```

**Solution Using IIFE**:
```javascript
for (var i = 1; i <= 5; i++) {
  (function(i) {
    setTimeout(function() {
      console.log(i);
    }, i * 1000);
  })(i);
}
// Output: 1, 2, 3, 4, 5 (each after respective seconds)
```

### Detailed Flowchart:

**1. Issue with Closures in Loops**:
   - `var` declarations are function-scoped, causing all `setTimeout` callbacks to reference the same variable.

```plaintext
for (var i = 1; i <= 5; i++) {
  setTimeout(callback, delay);
}
+---------------------------+
| Loop Iteration            |
|---------------------------|
| i = 1, callback scheduled |
| i = 2, callback scheduled |
| i = 3, callback scheduled |
| i = 4, callback scheduled |
| i = 5, callback scheduled |
| i = 6                     |
+---------------------------+
```

**2. Using IIFE to Solve the Issue**:
   - Immediately Invoked Function Expressions (IIFE) create a new scope for each iteration.

```plaintext
for (var i = 1; i <= 5; i++) {
  (function(i) {
    setTimeout(callback, delay);
  })(i);
}
+---------------------------+
| Loop Iteration            |
|---------------------------|
| i = 1, IIFE creates scope |
| i = 2, IIFE creates scope |
| i = 3, IIFE creates scope |
| i = 4, IIFE creates scope |
| i = 5, IIFE creates scope |
+---------------------------+
```

For a deeper understanding, please watch the video on [YouTube](https://www.youtube.com/watch?v=eBTBG4nda2A&list=PLlasXeu85E9cQ32gLCvAvr9vNaUccPVNP&index=13).
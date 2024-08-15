### Summary of "BLOCK SCOPE & Shadowing in JS 🔥| Namaste JavaScript 🙏 Ep. 9"

#### Key Points:

1. **Block Scope**:
   - Introduced in ES6 with `let` and `const`.
   - Variables declared inside a block (`{}`) cannot be accessed from outside the block.

2. **Variable Shadowing**:
   - When a variable declared in an inner scope has the same name as a variable in an outer scope, the inner variable shadows the outer one.

3. **Global vs. Local Scope**:
   - Global variables can be shadowed by local variables with the same name in inner scopes.

#### Code Examples:

**Example 1: Block Scope with `let` and `const`**:
```javascript
{
  let x = 10;
  const y = 20;
  console.log(x);  // Output: 10
  console.log(y);  // Output: 20
}
console.log(x);  // ReferenceError: x is not defined
console.log(y);  // ReferenceError: y is not defined
```

**Example 2: Variable Shadowing**:
```javascript
let a = 5;
{
  let a = 10;
  console.log(a);  // Output: 10 (inner scope)
}
console.log(a);  // Output: 5 (outer scope)
```

### Detailed Flowchart:

**1. Block Scope Execution**:

```plaintext
Global Execution Context:
+-----------------------------+
| Global Object               |
| let x                       |
+-----------------------------+

Block Execution Context:
+-----------------------------+
| let x = 10                  |
| const y = 20                |
+-----------------------------+
```

**2. Variable Shadowing Execution**:

```plaintext
Global Context:
+----------------------+
| a = 5                |
+----------------------+

Block Context:
+----------------------+
| a = 10 (shadows)     |
+----------------------+
```

For a more detailed explanation, please watch the video on [YouTube](https://www.youtube.com/watch?v=lW_erSjyMeM&list=PLlasXeu85E9cQ32gLCvAvr9vNaUccPVNP&index=10).
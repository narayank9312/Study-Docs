### Summary of "Execution Context & Call Stack | Namaste JavaScript Ep. 4" by Akshay Saini

#### Key Points:

1. **Execution Context**:
   - Represents the environment in which JavaScript code is executed.
   - Comprises the Global Execution Context and Function Execution Contexts.
   - Contains three main components:
     - **Variable Object (VO)**: Stores function arguments, variables, and function declarations.
     - **Scope Chain**: Consists of the current execution context's Variable Object and its parent execution context's Variable Objects.
     - **this**: Refers to the object that the function is executing in.

2. **Global Execution Context**:
   - Created when JavaScript starts execution.
   - Has a global object (e.g., `window` in browsers) and `this` points to the global object.

3. **Function Execution Context**:
   - Created whenever a function is called.
   - Each function call creates a new execution context.
   - Includes its own Variable Object, Scope Chain, and `this`.

4. **Call Stack**:
   - Manages the order of execution contexts using a Last-In-First-Out (LIFO) structure.
   - When a function is invoked, a new execution context is created and pushed onto the call stack.
   - Once the function execution is completed, the execution context is popped off the call stack.

### Detailed Flowchart:

**1. Global Execution Context Creation:**

```plaintext
Global Execution Context:
+--------------------------+
| Global Object (window)   |
| this = window            |
| Variable Object (VO)     |
| - globalVar              |
| - globalFunction         |
+--------------------------+
```

**2. Function Execution Context Creation:**

```plaintext
function foo() {
  console.log("Inside foo");
}
foo();

Call Stack:
+--------------------------+
| foo() Execution Context  |
| - VO                     |
| - Scope Chain            |
| - this                   |
|--------------------------|
| Global Execution Context |
| - VO                     |
| - Scope Chain            |
| - this                   |
+--------------------------+

Execution order:
1. foo() Execution Context created and pushed onto the Call Stack.
2. Global Execution Context remains at the bottom.
```

**3. Nested Function Calls:**

```javascript
function bar() {
  console.log("Inside bar");
  foo();
}
bar();

Call Stack:
+--------------------------+
| foo() Execution Context  |
| - VO                     |
| - Scope Chain            |
| - this                   |
|--------------------------|
| bar() Execution Context  |
| - VO                     |
| - Scope Chain            |
| - this                   |
|--------------------------|
| Global Execution Context |
| - VO                     |
| - Scope Chain            |
| - this                   |
+--------------------------+

Execution order:
1. bar() Execution Context created and pushed onto the Call Stack.
2. foo() Execution Context created and pushed onto the Call Stack.
3. foo() Execution Context popped after completion.
4. bar() Execution Context popped after completion.
```

### Code Examples:

**Example 1: Global and Function Execution Contexts**:
```javascript
var globalVar = "I am a global variable";

function globalFunction() {
  var localVar = "I am a local variable";
  console.log(localVar);
}

globalFunction();
console.log(globalVar);
```

**Example 2: Nested Function Calls**:
```javascript
function foo() {
  console.log("Inside foo");
}

function bar() {
  console.log("Inside bar");
  foo();
}

bar();
```

These diagrams and flowcharts illustrate how the JavaScript engine handles execution contexts and the call stack during the compilation and execution phases.

For a detailed understanding, watch the video [here](https://www.youtube.com/watch?v=gSDncyuGw0s&list=PLlasXeu85E9cQ32gLCvAvr9vNaUccPVNP&index=5).
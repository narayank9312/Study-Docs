### Summary of "How JavaScript Code is executed? ❤️& Call Stack | Namaste JavaScript Ep. 2"

#### Key Points:

1. **JavaScript Engine**: 
   - The JavaScript engine (like V8) compiles and executes JavaScript code.
   - It includes components like the Call Stack and the Heap.

2. **Call Stack**:
   - Manages the execution context of functions using a Last-In-First-Out (LIFO) structure.
   - When a function is called, it’s pushed onto the stack; once executed, it’s popped off.

3. **Execution Context**:
   - Created for global and function code execution.
   - Includes `Variable Environment`, `Lexical Environment`, and `this` binding.

4. **Memory Heap**:
   - Allocates memory for objects and functions.

#### Diagram and Flowchart

**1. JavaScript Engine Components:**

```plaintext
+-------------------+
| Memory Heap       |
|-------------------|
| Object Allocation |
+-------------------+

+-------------------+
| Call Stack        |
|-------------------|
| Function Calls    |
+-------------------+
```

**2. Call Stack Execution:**

```plaintext
function greet() {
  console.log("Hello");
}

greet();

+-------------------+
| Call Stack        |
|-------------------|
| greet()           |
| console.log()     |
+-------------------+

Execution order:
1. greet()
2. console.log("Hello")
```

For more details, watch the video [here](https://www.youtube.com/watch?v=iLWTnMzWtj4&list=PLlasXeu85E9cQ32gLCvAvr9vNaUccPVNP&index=3).
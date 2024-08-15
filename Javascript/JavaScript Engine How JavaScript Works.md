### Summary of "JavaScript Engine: How JavaScript Works" by Akshay Saini

The video explains how the JavaScript engine executes code, focusing on V8 (used in Chrome and Node.js). Key components include:

1. **Call Stack**: Manages function execution using a Last-In-First-Out (LIFO) structure.
2. **Heap**: Memory allocation for objects.
3. **Event Loop**: Handles asynchronous operations, checking the Call Stack and Callback Queue.
4. **Web APIs**: Browser-provided APIs for async operations.
5. **Callback Queue**: Holds async callbacks to be executed by the Event Loop.

### Diagram and Flowchart

1. **Initial Code Execution**:
   - Code is parsed and executed by the Call Stack.
   - Functions and variables are allocated memory.

```plaintext
+-------------------+
| Call Stack        |
|-------------------|
| Global Context    |
|-------------------|
```

2. **Asynchronous Operations**:
   - Asynchronous functions (e.g., `setTimeout`) are handled by Web APIs.
   - After completion, callbacks are placed in the Callback Queue.

```plaintext
+-------------------+      +-------------------+      +-------------------+
| Call Stack        |      | Web APIs          |      | Callback Queue    |
|-------------------|      |-------------------|      |-------------------|
| console.log('Hi') | -->  | setTimeout(fn, 0) | ---> | function fn()     |
|-------------------|      |                   |      |                   |
+-------------------+      +-------------------+      +-------------------+
```

3. **Event Loop Process**:
   - Event Loop checks if the Call Stack is empty.
   - If empty, it moves the first callback from the Callback Queue to the Call Stack.

```plaintext
+-------------------+
| Call Stack        |
|-------------------|
| function fn()     |
|-------------------|
```

For a detailed understanding, you can watch the full video [here](https://www.youtube.com/watch?v=ZvbzSrg0afE&list=PLlasXeu85E9cQ32gLCvAvr9vNaUccPVNP&index=2).
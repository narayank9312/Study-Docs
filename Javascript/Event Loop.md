To summarize the main points from the video titled "Event Loop | Namaste JavaScript Ep. 6" by Akshay Saini and help you understand the content with diagrams and flowcharts, here’s a detailed explanation:

### Key Points:

1. **Event Loop**:
   - The event loop allows JavaScript to perform non-blocking operations by offloading operations to the system kernel whenever possible.
   - It checks the call stack and task queue to see if there are any functions to execute.

2. **Call Stack**:
   - The call stack is where the execution context is pushed and popped.
   - Functions are pushed to the call stack when they are invoked and popped when they return.

3. **Web APIs**:
   - Web APIs handle asynchronous operations like `setTimeout`, `DOM events`, `AJAX`, etc.
   - After completion, the callback is sent to the task queue.

4. **Task Queue**:
   - The task queue holds the callbacks for asynchronous operations.
   - The event loop moves tasks from the task queue to the call stack when the stack is empty.

5. **Microtask Queue**:
   - Microtasks (like `Promises`) are prioritized over tasks in the task queue.
   - They are executed after the currently executing script and before the next rendering.

### Code Examples:

**Example 1: setTimeout and Event Loop**:
```javascript
console.log('Start');

setTimeout(() => {
  console.log('Callback');
}, 0);

console.log('End');

// Output:
// Start
// End
// Callback
```

**Example 2: Promises and Microtasks**:
```javascript
console.log('Start');

Promise.resolve().then(() => {
  console.log('Promise');
});

console.log('End');

// Output:
// Start
// End
// Promise
```

### Detailed Flowchart:

**1. Event Loop Execution**:

**Initialization**:
```plaintext
+---------------------------+
| Call Stack                |
|---------------------------|
| Global Execution Context  |
+---------------------------+
| Web APIs                  |
|---------------------------|
| Task Queue                |
|---------------------------|
| Microtask Queue           |
+---------------------------+
```

**2. Handling setTimeout**:
1. **Call Stack**:
   ```plaintext
   +---------------------------+
   | setTimeout()              |
   |---------------------------|
   | Global Execution Context  |
   +---------------------------+
   ```
2. **Web APIs**:
   ```plaintext
   +---------------------------+
   | Call Stack                |
   |---------------------------|
   | Web APIs                  |
   | setTimeout                |
   +---------------------------+
   ```
3. **Task Queue**:
   ```plaintext
   +---------------------------+
   | Call Stack                |
   |---------------------------|
   | Task Queue                |
   | callback                  |
   +---------------------------+
   ```

**3. Handling Promises**:
1. **Call Stack**:
   ```plaintext
   +---------------------------+
   | Promise.then()            |
   |---------------------------|
   | Global Execution Context  |
   +---------------------------+
   ```
2. **Microtask Queue**:
   ```plaintext
   +---------------------------+
   | Call Stack                |
   |---------------------------|
   | Microtask Queue           |
   | Promise callback          |
   +---------------------------+
   ```

For more detailed understanding, please watch the video on [YouTube](https://www.youtube.com/watch?v=uH-tVP8MUs8).
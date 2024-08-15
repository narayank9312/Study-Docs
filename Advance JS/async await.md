### Summary of "async await | Namaste JavaScript - Season 02 - Ep 04"

1. **Introduction to Async/Await**
   - Brief recap of promises and callback hell.
   - Introduction to async/await as a simpler, cleaner way to handle asynchronous code.

2. **Async Functions**
   - How to declare an async function using the `async` keyword.
   - Async functions always return a promise.

3. **Using the Await Keyword**
   - The `await` keyword pauses the execution of an async function until the promise is resolved.
   - Explanation of how `await` can be used to write asynchronous code that looks synchronous.

4. **Error Handling with Try/Catch**
   - Using `try/catch` blocks to handle errors in async functions.
   - Example demonstrating error handling with async/await.

5. **Sequential vs Parallel Execution**
   - Demonstrating the difference between sequential and parallel execution of async tasks.
   - Using `Promise.all()` with async/await for parallel execution.

### Diagrams and Flowcharts

#### Async/Await Flowchart
```plaintext
Start
  |
async function()
  |
await promise
  |
.then(result => handleResult)
  |
.catch(error => handleError)
  |
End
```

#### Sequential Execution Flowchart
```plaintext
Start
  |
await asyncTask1()
  |
await asyncTask2()
  |
await asyncTask3()
  |
End
```

#### Parallel Execution Flowchart
```plaintext
Start
  |
Promise.all([
  asyncTask1(),
  asyncTask2(),
  asyncTask3()
])
  |
.then(results => handleResults)
  |
.catch(error => handleError)
  |
End
```

### Example Code

#### Basic Async/Await Example
```javascript
async function fetchData() {
    try {
        let response = await fetch('https://api.example.com/data');
        let data = await response.json();
        console.log(data);
    } catch (error) {
        console.error('Error fetching data:', error);
    }
}

fetchData();
```

#### Sequential Execution Example
```javascript
async function sequentialTasks() {
    try {
        let result1 = await task1();
        console.log(result1);
        
        let result2 = await task2();
        console.log(result2);
        
        let result3 = await task3();
        console.log(result3);
    } catch (error) {
        console.error('Error:', error);
    }
}

sequentialTasks();
```

#### Parallel Execution Example
```javascript
async function parallelTasks() {
    try {
        let [result1, result2, result3] = await Promise.all([
            task1(),
            task2(),
            task3()
        ]);
        
        console.log(result1, result2, result3);
    } catch (error) {
        console.error('Error:', error);
    }
}

parallelTasks();
```

These points, diagrams, and code examples provide a comprehensive understanding of async/await as covered in the video. If you have specific questions or need further clarification on any part, feel free to ask!
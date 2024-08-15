### Useful Promise Methods

#### `Promise.all()`
- Takes an array of promises and returns a single promise.
- Resolves when all promises in the array have resolved.
- Rejects if any promise in the array rejects.

**Example:**
```javascript
Promise.all([promise1, promise2, promise3])
  .then(results => {
    console.log(results); // Array of results
  })
  .catch(error => {
    console.error(error); // First error encountered
  });
```

#### `Promise.race()`
- Takes an array of promises and returns a single promise.
- Resolves or rejects as soon as one of the promises in the array resolves or rejects.

**Example:**
```javascript
Promise.race([promise1, promise2, promise3])
  .then(result => {
    console.log(result); // First resolved value
  })
  .catch(error => {
    console.error(error); // First error encountered
  });
```

#### `Promise.allSettled()`
- Takes an array of promises and returns a single promise.
- Resolves when all promises in the array have settled (either resolved or rejected).
- Provides an array of objects describing the outcome of each promise.

**Example:**
```javascript
Promise.allSettled([promise1, promise2, promise3])
  .then(results => {
    results.forEach(result => {
      if (result.status === "fulfilled") {
        console.log(result.value);
      } else {
        console.error(result.reason);
      }
    });
  });
```

#### `Promise.any()`
- Takes an array of promises and returns a single promise.
- Resolves as soon as one of the promises in the array resolves.
- Rejects only if all promises in the array reject.

**Example:**
```javascript
Promise.any([promise1, promise2, promise3])
  .then(result => {
    console.log(result); // First resolved value
  })
  .catch(error => {
    console.error(error); // AggregateError if all reject
  });
```

### Diagrams and Flowcharts

#### `Promise.all()` Flowchart
```plaintext
Start
  |
Promise1 ----
  |          |
Promise2 ----|----- .all() --> .then(results) --> Handle results
  |          |
Promise3 ----|
  |
.catch(error)
  |
End
```

#### `Promise.race()` Flowchart
```plaintext
Start
  |
Promise1 ----
  |          |
Promise2 ----|----- .race() --> .then(result) --> Handle result
  |          |
Promise3 ----|
  |
.catch(error)
  |
End
```

#### `Promise.allSettled()` Flowchart
```plaintext
Start
  |
Promise1 ----
  |          |
Promise2 ----|----- .allSettled() --> .then(results) --> Handle each result
  |          |
Promise3 ----|
  |
End
```

#### `Promise.any()` Flowchart
```plaintext
Start
  |
Promise1 ----
  |          |
Promise2 ----|----- .any() --> .then(result) --> Handle result
  |          |
Promise3 ----|
  |
.catch(AggregateError)
  |
End
```

These methods help manage multiple asynchronous operations efficiently and improve code readability. If you need further explanation or additional examples, feel free to ask!
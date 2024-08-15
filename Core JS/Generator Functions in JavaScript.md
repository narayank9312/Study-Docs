### Generator Functions in JavaScript

**Concept**:
Generator functions are special functions that can pause execution and resume later. They allow you to define an iterative algorithm by writing a function whose execution is not continuous.

### Syntax:

```javascript
function* generatorFunction() {
  yield 'Hello';
  yield 'World';
  return 'Done';
}
```

### Example:

```javascript
function* numbersGenerator() {
  yield 1;
  yield 2;
  yield 3;
}

const gen = numbersGenerator();
console.log(gen.next().value); // Output: 1
console.log(gen.next().value); // Output: 2
console.log(gen.next().value); // Output: 3
console.log(gen.next().value); // Output: undefined
```

### Explanation:
1. **`function*`**: Defines a generator function.
2. **`yield`**: Pauses the function execution and returns a value.
3. **`next()`**: Resumes the function execution, returning an object with `value` and `done` properties.

### Use Cases:
- Iterating over large datasets.
- Implementing iterators.
- Managing asynchronous operations.

Generator functions provide a powerful way to manage control flow, particularly useful for handling asynchronous tasks or implementing custom iterators.
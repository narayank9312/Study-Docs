Sure! Here is a deep dive into each topic with practical examples:

### 1. Hoisting
**Concept**: Variable and function declarations are moved to the top of their containing scope during compile time.
**Example**:
```javascript
console.log(a); // undefined
var a = 5;

foo(); // "Hello"
function foo() {
  console.log("Hello");
}
```
### 2. Objects (Referencing, Copying, Cloning)
**Concept**: Objects in JS are stored by reference.
**Example**:
```javascript
let obj1 = { a: 1 };
let obj2 = obj1; // obj2 references obj1
obj2.a = 2;
console.log(obj1.a); // 2

let obj3 = { ...obj1 }; // Cloning
obj3.a = 3;
console.log(obj1.a); // 2
```

### 3. `this` Keyword
**Concept**: Refers to the object it belongs to.
**Example**:
```javascript
const obj = {
  value: 42,
  getValue() {
    return this.value;
  }
};
console.log(obj.getValue()); // 42
```

### 4. Functions
**Arrow Functions**:
```javascript
const add = (a, b) => a + b;
console.log(add(2, 3)); // 5
```
**Function Expressions**:
```javascript
const greet = function() {
  return 'Hello';
};
console.log(greet()); // "Hello"
```
**IIFE**:
```javascript
(function() {
  console.log("IIFE");
})();
```

### 5. Array Methods
**map, filter, reduce**:
```javascript
const arr = [1, 2, 3, 4, 5];
const mapped = arr.map(x => x * 2); // [2, 4, 6, 8, 10]
const filtered = arr.filter(x => x > 2); // [3, 4, 5]
const reduced = arr.reduce((acc, x) => acc + x, 0); // 15
```

### 6. `var`, `let`, and `const`
**Scope Differences**:
```javascript
var x = 1;
if (true) {
  var x = 2;
}
console.log(x); // 2

let y = 1;
if (true) {
  let y = 2;
}
console.log(y); // 1

const z = 1;
z = 2; // Error
```

### 7. Event Loop and Execution Context
**Concept**: Handles asynchronous operations in JS.
**Example**:
```javascript
console.log("Start");
setTimeout(() => {
  console.log("Timeout");
}, 0);
console.log("End");
// Output: "Start", "End", "Timeout"
```

### 8. map, filter, and reduce
**Example**:
```javascript
const nums = [1, 2, 3];
const doubled = nums.map(n => n * 2); // [2, 4, 6]
const even = nums.filter(n => n % 2 === 0); // [2]
const sum = nums.reduce((acc, n) => acc + n, 0); // 6
```

### 9. Event Bubbling/Capturing/Delegation
**Example**:
```javascript
document.querySelector("#parent").addEventListener("click", () => {
  console.log("Parent clicked!");
}, true); // capturing

document.querySelector("#child").addEventListener("click", () => {
  console.log("Child clicked!");
}); // bubbling

document.querySelector("#container").addEventListener("click", (e) => {
  if (e.target.matches(".item")) {
    console.log("Item clicked!");
  }
}); // delegation
```

### 10. call, bind, apply
**Example**:
```javascript
const person = {
  name: 'Alice',
  greet() {
    console.log(`Hello, ${this.name}`);
  }
};

const anotherPerson = { name: 'Bob' };
person.greet.call(anotherPerson); // Hello, Bob
person.greet.apply(anotherPerson); // Hello, Bob

const boundGreet = person.greet.bind(anotherPerson);
boundGreet(); // Hello, Bob
```

### 11. Prototypal Inheritance
**Example**:
```javascript
function Person(name) {
  this.name = name;
}

Person.prototype.greet = function() {
  console.log(`Hello, ${this.name}`);
};

const alice = new Person('Alice');
alice.greet(); // Hello, Alice
```

### 12. Debouncing/Throttling
**Debouncing**:
```javascript
function debounce(func, delay) {
  let debounceTimer;
  return function(...args) {
    clearTimeout(debounceTimer);
    debounceTimer = setTimeout(() => func.apply(this, args), delay);
  };
}
```
**Throttling**:
```javascript
function throttle(func, limit) {
  let inThrottle;
  return function(...args) {
    if (!inThrottle) {
      func.apply(this, args);
      inThrottle = true;
      setTimeout(() => inThrottle = false, limit);
    }
  };
}
```

### 13. Callbacks
**Example**:
```javascript
function fetchData(callback) {
  setTimeout(() => {
    callback("Data fetched");
  }, 1000);
}

fetchData(data => {
  console.log(data);
});
```

### 14. Promises, async/await
**Promises**:
```javascript
const promise = new Promise((resolve, reject) => {
  setTimeout(() => resolve("Resolved!"), 1000);
});

promise.then(result => console.log(result));
```
**async/await**:
```javascript
async function fetchData() {
  const result = await new Promise(resolve => setTimeout(() => resolve("Resolved!"), 1000));
  console.log(result);
}

fetchData();
```

### 15. Currying
**Example**:
```javascript
function add(a) {
  return function(b) {
    return a + b;
  };
}

const addFive = add(5);
console.log(addFive(10)); // 15
```

### 16. Scopes
**Example**:
```javascript
let x = 'global';

function outer() {
  let x = 'outer';
  
  function inner() {
    let x = 'inner';
    console.log(x); // inner
  }

  inner();
  console.log(x); // outer
}

outer();
console.log(x); // global
```

### 17. Memoization
**Example**:
```javascript
function memoize(fn) {
  const cache = {};
  return function(...args) {
    const key = JSON.stringify(args);
    if (cache[key]) {
      return cache[key];
    }
    const result = fn(...args);
    cache[key] = result;
    return result;
  };
}

const factorial = memoize(function(n) {
  if (n === 0) return 1;
  return n * factorial(n - 1);
});

console.log(factorial(5)); // 120
```

### 18. Micro/Macro Tasks
**Concept**: Microtasks have higher priority and are executed before macrotasks.
**Example**:
```javascript
console.log("Start");

setTimeout(() => {
  console.log("Macrotask");
}, 0);

Promise.resolve().then(() => {
  console.log("Microtask");
});

console.log("End");
// Output: "Start", "End", "Microtask", "Macrotask"
```

### 19. Closures
**Example**:
```javascript
function outer() {
  let count = 0;
  return function() {
    count++;
    console.log(count);
  };
}

const increment = outer();
increment(); // 1
increment(); // 2
```

### 20. Memoization
See above under 17.

### 21. setTimeout vs setInterval
**setTimeout**: Executes a function once after a delay.
**setInterval**: Repeatedly executes a function with a fixed time delay.
**Example**:
```javascript
setTimeout(() => {
  console.log("Timeout");
}, 1000);

const interval = setInterval(() => {
  console.log("Interval");
  clearInterval(interval); // Stops after one iteration
}, 1000);
```

### 22. JS Engine & Execution Context
**Concept**: JS engine compiles and executes JavaScript code. Execution context contains the environment in which the code is executed.
**Example**:
```javascript
console.log("Execution Context Example");
```

### 23. Higher-Order Functions (HOF)
**Concept**: Functions that take other functions as arguments or return them.
**Example**:
```javascript
function greet(name) {
  return function(message) {
    console.log(`${name}, ${message}`);
  };
}

const greetJohn = greet("John");
greetJohn("Good morning!"); // "John, Good morning!"
```

### 24. Async & Defer
**Async**: Downloads script while the rest of the page continues to load. Executes as soon as it's available.
**Defer**: Downloads script while the page continues to load. Executes after the page has finished loading.
**Example**:
```html
<script src="script.js" async></script>
<script src="script.js" defer></script>
```

### 25. Math & Date Objects
**Example**:
```javascript
console.log(Math.max(1, 2, 3

### Math & Date Objects in JavaScript

#### Math Object
**Example**:
```javascript
console.log(Math.max(1, 2, 3)); // 3
console.log(Math.min(1, 2, 3)); // 1
console.log(Math.sqrt(16)); // 4
console.log(Math.random()); // Random number between 0 and 1
```

#### Date Object
**Example**:
```javascript
const now = new Date();
console.log(now); // Current date and time

const specificDate = new Date('2024-06-11T12:00:00');
console.log(specificDate); // Specified date and time

console.log(now.getFullYear()); // Current year
console.log(now.getMonth()); // Current month (0-based)
console.log(now.getDate()); // Current day of the month
```

### Summary of Topics

1. **Hoisting**: Variable and function declarations are moved to the top.
2. **Objects**: Reference, copy, clone.
3. **`this` keyword**: Context-specific reference.
4. **Functions**: Arrow, function expressions, IIFE.
5. **Array Methods**: `map`, `filter`, `reduce`.
6. **`var`, `let`, `const`**: Scope and reassignment rules.
7. **Event Loop & Execution Context**: Handles asynchronous operations.
8. **Event Handling**: Bubbling, capturing, delegation.
9. **Function Methods**: `call`, `bind`, `apply`.
10. **Inheritance**: Prototypal inheritance.
11. **Optimization**: Debouncing, throttling.
12. **Asynchronous Programming**: Callbacks, promises, async/await.
13. **Functional Techniques**: Currying, memoization, closures.
14. **Task Handling**: Micro/macro tasks.
15. **Timers**: `setTimeout` vs. `setInterval`.
16. **JavaScript Engine**: Execution context.
17. **Higher-Order Functions**: Functions as arguments/return values.
18. **Script Loading**: `async` and `defer`.
19. **Utility Objects**: Math and Date objects.
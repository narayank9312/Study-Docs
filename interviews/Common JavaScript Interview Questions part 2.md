### Detailed Explanation and Practical Examples for JavaScript Topics

#### a. Lexical Scoping
**Explanation:** Lexical scoping means a variable's scope is determined by its position in the source code. Inner functions have access to variables defined in their outer scope.

**Example:**
```javascript
function outer() {
    let outerVar = 'I am outside!';
    function inner() {
        let innerVar = 'I am inside!';
        console.log(outerVar); // Accessible
    }
    inner();
    console.log(innerVar); // Error: innerVar is not defined
}
outer();
```

#### b. Hoisting, Temporal Dead Zone
**Explanation:** Hoisting is JavaScript's default behavior of moving declarations to the top. The Temporal Dead Zone (TDZ) is the time between entering a scope and declaring a variable, during which the variable cannot be accessed.

**Example:**
```javascript
console.log(a); // undefined due to hoisting
var a = 5;

console.log(b); // ReferenceError due to TDZ
let b = 10;
```

#### c. Closure
**Explanation:** A closure is a function that retains access to its lexical scope, even when the function is executed outside that scope.

**Example:**
```javascript
function outerFunction(outerVariable) {
    return function innerFunction(innerVariable) {
        console.log('Outer:', outerVariable);
        console.log('Inner:', innerVariable);
    };
}
const newFunction = outerFunction('outside');
newFunction('inside');
```

#### d. ES6 Features
**Explanation:** ES6 introduced several features, such as `let` and `const` for block scoping, template literals for string interpolation, destructuring for easy extraction of values from arrays or objects, promises for handling asynchronous operations, and classes for easier object-oriented programming.

**Example:**
```javascript
// let, const
const name = 'John';
let age = 25;

// Template literals
console.log(`Hello, ${name}! You are ${age} years old.`);

// Destructuring
const person = { name: 'John', age: 25 };
const { name: personName, age: personAge } = person;
console.log(personName, personAge);

// Promises
const promise = new Promise((resolve, reject) => {
    setTimeout(() => resolve('Done!'), 1000);
});
promise.then(result => console.log(result));

// Classes
class Person {
    constructor(name) {
        this.name = name;
    }
    greet() {
        console.log(`Hello, ${this.name}!`);
    }
}
const john = new Person('John');
john.greet();
```

#### e. Is JavaScript Asynchronous Language?
**Explanation:** JavaScript is single-threaded and synchronous by default. However, it can be asynchronous through mechanisms like callbacks, promises, and async/await, which allow non-blocking operations.

#### f. Events in JS? Event Bubbling and Capturing?
**Explanation:** Events are actions triggered by the user or browser. Event bubbling and capturing are phases of event propagation in the DOM. Bubbling propagates from the target element up to the root, while capturing goes from the root to the target.

**Example:**
```javascript
document.getElementById('child').addEventListener('click', () => {
    console.log('Child clicked');
}, false); // Bubbling

document.getElementById('parent').addEventListener('click', () => {
    console.log('Parent clicked');
}, true); // Capturing
```

#### g. Difference between Web Worker and Service Worker
**Explanation:** Web Workers run scripts in background threads, enhancing performance by offloading tasks from the main thread. Service Workers act as proxies between web apps and the network, enabling features like offline support and background sync.

#### h. Write a Memoization Function
**Explanation:** Memoization is an optimization technique that stores the results of expensive function calls and returns the cached result when the same inputs occur again.

**Example:**
```javascript
function memoize(fn) {
    const cache = {};
    return function(...args) {
        const key = JSON.stringify(args);
        if (cache[key]) {
            return cache[key];
        } else {
            const result = fn(...args);
            cache[key] = result;
            return result;
        }
    };
}

const factorial = memoize(function(n) {
    if (n === 0) return 1;
    return n * factorial(n - 1);
});

console.log(factorial(5)); // 120
```

#### i. `this` in JS
**Explanation:** The `this` keyword refers to the object it belongs to. In the global context, `this` refers to the global object (window in browsers). In methods, `this` refers to the object calling the method. In constructors, `this` refers to the instance being created.

#### j. Prototype and Prototypal Inheritance
**Explanation:** Every JavaScript object has a prototype, from which it inherits properties and methods. Prototypal inheritance allows objects to inherit directly from other objects.

**Example:**
```javascript
function Person(name) {
    this.name = name;
}
Person.prototype.greet = function() {
    console.log(`Hello, ${this.name}!`);
};
const john = new Person('John');
john.greet(); // Hello, John!
```

#### k. How Browsers Work When You Hit a URL?
**Explanation:** When a URL is typed and entered, the browser parses the URL, performs DNS lookup, establishes a TCP connection, sends an HTTP request, receives the response, and then renders the content.

**Resources:**
- [What happens when you type an URL in the browser and press enter](https://medium.com/@maneesa/what-happens-when-you-type-an-url-in-the-browser-and-press-enter-bb0aa2449c1a)
- [Video](https://youtu.be/MOd5cTJ6kaA)

#### l. Local Storage vs Session Storage vs Cookies
**Explanation:** 
- **Local Storage:** Stores data with no expiration date.
- **Session Storage:** Stores data for the duration of the page session.
- **Cookies:** Store data that is sent to the server with every HTTP request.

#### m. Web APIs like `setTimeout` & `setInterval`
**Explanation:** 
- **`setTimeout`:** Executes a function after a specified delay.
- **`setInterval`:** Repeatedly executes a function with a fixed time delay between each call.

**Example:**
```javascript
setTimeout(() => {
    console.log('Executed after 2 seconds');
}, 2000);

const intervalId = setInterval(() => {
    console.log('Executed every 1 second');
}, 1000);

// To clear the interval
clearInterval(intervalId);
```

#### n. Infinite Scroll
**Explanation:** Infinite scroll is a web design technique that loads more content as the user scrolls down the page, creating an endless scrolling experience.

**Example:**
```javascript
window.addEventListener('scroll', () => {
    if (window.innerHeight + window.scrollY >= document.body.offsetHeight) {
        // Load more content
    }
});
```

### Polyfills/ Implementation-based Questions

#### a. Promise.all(), Promise.any()
**Explanation:** 
- **`Promise.all()`:** Resolves when all promises resolve or rejects if any promise rejects.
- **`Promise.any()`:** Resolves as soon as one of the promises resolves or rejects if all promises reject.

**Example:**
```javascript
const promise1 = Promise.resolve(3);
const promise2 = 42;
const promise3 = new Promise((resolve, reject) => setTimeout(resolve, 100, 'foo'));

Promise.all([promise1, promise2, promise3]).then(values => {
  console.log(values); // [3, 42, "foo"]
});

Promise.any([promise1, promise2, promise3]).then(value => {
  console.log(value); // 'quick'
});
```

#### b. Clear All Timeouts
**Explanation:** Clearing all timeouts involves keeping track of all timeout IDs and then clearing each one.

**Example:**
```javascript
const timeouts = [];
for (let i = 0; i < 10; i++) {
    timeouts.push(setTimeout(() => console.log(i), i * 1000));
}
timeouts.forEach(clearTimeout);
```

#### c. Flat Array `Array.flat()` in Both Recursive and Iterative Ways
**Explanation:**
- **Recursive:** Flatten the array using recursion.
- **Iterative:** Flatten the array using an iterative approach.

**Example:**
```javascript
// Recursive
function flatRecursive(arr) {
    return arr.reduce((acc, val) => Array.isArray(val) ? acc.concat(flatRecursive(val)) : acc.concat(val), []);
}
console.log(flatRecursive([1, [2, [3, 4], 5]])); // [1, 2, 3, 4, 5]

// Iterative
function flatIterative(arr) {
    const stack = [...arr];
    const result = [];
    while (stack.length) {
        const next = stack.pop();
        if (Array.isArray(next)) {
            stack.push(...next);
        } else {
            result.push(next);
        }
    }
    return result.reverse();
}
console.log(flatIterative([1, [2, [3, 4], 5]])); // [1, 2, 3, 4, 5]
```

#### d. Flatten Object
**Explanation:** Flatten a nested object by converting it to a single-level object with dot-separated keys.

**Example:**
```javascript
function flattenObject(obj, parent = '', res = {}) {
    for (let key in obj) {
        let

#### Detailed Explanation and Practical Examples for JavaScript Topics

### Polyfills/ Implementation-based Questions

#### a. Promise.all(), Promise.any()
**Explanation:**
- **Promise.all()**: Resolves when all promises resolve or rejects if any promise rejects.
- **Promise.any()**: Resolves as soon as one of the promises resolves or rejects if all promises reject.

**Example:**
```javascript
// Promise.all()
const promise1 = Promise.resolve(3);
const promise2 = 42;
const promise3 = new Promise((resolve) => setTimeout(resolve, 100, 'foo'));

Promise.all([promise1, promise2, promise3]).then(values => {
  console.log(values); // [3, 42, "foo"]
});

// Promise.any()
const promise4 = Promise.reject(0);
const promise5 = new Promise((resolve) => setTimeout(resolve, 100, 'quick'));
const promise6 = new Promise((resolve) => setTimeout(resolve, 500, 'slow'));

Promise.any([promise4, promise5, promise6]).then(value => {
  console.log(value); // 'quick'
}).catch(error => {
  console.error('All promises were rejected');
});
```

#### b. Clear All Timeouts
**Explanation:** Track all timeout IDs and clear them to stop all pending timeouts.

**Example:**
```javascript
const timeouts = [];
for (let i = 0; i < 10; i++) {
    timeouts.push(setTimeout(() => console.log(i), i * 1000));
}
timeouts.forEach(clearTimeout);
```

#### c. Flat Array `Array.flat()` in Both Recursive and Iterative Ways
**Explanation:** Flatten an array using both recursive and iterative approaches.

**Example:**
```javascript
// Recursive
function flatRecursive(arr) {
    return arr.reduce((acc, val) => Array.isArray(val) ? acc.concat(flatRecursive(val)) : acc.concat(val), []);
}
console.log(flatRecursive([1, [2, [3, 4], 5]])); // [1, 2, 3, 4, 5]

// Iterative
function flatIterative(arr) {
    const stack = [...arr];
    const result = [];
    while (stack.length) {
        const next = stack.pop();
        if (Array.isArray(next)) {
            stack.push(...next);
        } else {
            result.push(next);
        }
    }
    return result.reverse();
}
console.log(flatIterative([1, [2, [3, 4], 5]])); // [1, 2, 3, 4, 5]
```

#### d. Flatten Object
**Explanation:** Convert a nested object into a single-level object with dot-separated keys.

**Example:**
```javascript
function flattenObject(obj, parent = '', res = {}) {
    for (let key in obj) {
        let propName = parent ? `${parent}.${key}` : key;
        if (typeof obj[key] === 'object' && obj[key] !== null) {
            flattenObject(obj[key], propName, res);
        } else {
            res[propName] = obj[key];
        }
    }
    return res;
}
const nested = { a: { b: { c: 1 } }, d: 2 };
console.log(flattenObject(nested)); // { "a.b.c": 1, "d": 2 }
```

#### e. Pipe and Compose
**Explanation:**
- **Pipe**: Composes functions from left to right.
- **Compose**: Composes functions from right to left.

**Example:**
```javascript
// Pipe
const pipe = (...functions) => input => functions.reduce((acc, fn) => fn(acc), input);
const add = x => x + 1;
const multiply = x => x * 2;
const result = pipe(add, multiply)(5); // 12

// Compose
const compose = (...functions) => input => functions.reduceRight((acc, fn) => fn(acc), input);
const resultCompose = compose(multiply, add)(5); // 11
```

#### f. Higher Order Functions like Map, Reduce, Filter, Sort
**Explanation:** Functions that take other functions as arguments or return them as results.

**Example:**
```javascript
const arr = [1, 2, 3, 4, 5];
const mapped = arr.map(x => x * 2); // [2, 4, 6, 8, 10]
const filtered = arr.filter(x => x > 2); // [3, 4, 5]
const reduced = arr.reduce((acc, x) => acc + x, 0); // 15
const sorted = arr.sort((a, b) => b - a); // [5, 4, 3, 2, 1]
```

#### g. Call, Apply, Bind
**Explanation:**
- **Call**: Calls a function with a given `this` value and arguments.
- **Apply**: Calls a function with a given `this` value and arguments as an array.
- **Bind**: Returns a new function with a given `this` value and arguments.

**Example:**
```javascript
function greet(greeting, punctuation) {
    console.log(greeting + ', ' + this.name + punctuation);
}
const person = { name: 'John' };
greet.call(person, 'Hello', '!'); // Hello, John!
greet.apply(person, ['Hi', '?']); // Hi, John?
const greetPerson = greet.bind(person, 'Hey');
greetPerson('.'); // Hey, John.
```

#### h. Print Numbers 1 to 10 in a Time Interval of 1 Sec and Update on UI
**Explanation:** Print numbers from 1 to 10 at 1-second intervals and update them on the UI.

**Example:**
```javascript
let i = 1;
const interval = setInterval(() => {
    console.log(i);
    document.getElementById('number').innerText = i;
    if (i === 10) clearInterval(interval);
    i++;
}, 1000);
```

#### i. Debouncing and Throttling Solution
**Explanation:** 
- **Debouncing**: Delays the execution of a function until after a certain period of inactivity.
- **Throttling**: Ensures a function is called at most once in a specified period.

**Example:**
```javascript
// Debounce
function debounce(func, wait) {
    let timeout;
    return function(...args) {
        clearTimeout(timeout);
        timeout = setTimeout(() => func.apply(this, args), wait);
    };
}

// Throttle
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

#### j. Polyfill to Count Vowels in a String
**Explanation:** Adds a method to count the number of vowels in a string.

**Example:**
```javascript
String.prototype.countVowels = function() {
    return (this.match(/[aeiou]/gi) || []).length;
};
console.log("hello world".countVowels()); // 3
```

#### k. Implement Virtualization Table in JS
**Explanation:** A virtualized table renders only the visible rows, improving performance with large datasets.

**Example:**
```javascript
function VirtualizedTable({ rows, height, rowHeight }) {
    const [scrollTop, setScrollTop] = React.useState(0);
    const visibleRowCount = Math.ceil(height / rowHeight);
    const totalHeight = rows.length * rowHeight;
    const startIndex = Math.floor(scrollTop / rowHeight);
    const visibleRows = rows.slice(startIndex, startIndex + visibleRowCount);

    return (
        <div
            style={{ height, overflowY: 'auto' }}
            onScroll={e => setScrollTop(e.currentTarget.scrollTop)}
        >
            <div style={{ height: totalHeight, position: 'relative' }}>
                {visibleRows.map((row, index) => (
                    <div key={index} style={{ position: 'absolute', top: (startIndex + index) * rowHeight }}>
                        {row}
                    </div>
                ))}
            </div>
        </div>
    );
}
```

#### l. Method Chaining Solution
**Explanation:** Implement a class where methods return `this` to allow chaining.

**Example:**
```javascript
class Calculator {
    constructor(value = 0) {
        this.value = value;
    }
    add(val) {
        this.value += val;
        return this;
    }
    subtract(val) {
        this.value -= val;
        return this;
    }
    multiply(val) {
        this.value *= val;
        return this;
    }
    divide(val) {
        this.value /= val;
        return this;
    }
    getResult() {
        return this.value;
    }
}
const result = new Calculator(10).add(5).subtract(3).multiply(4).divide(2).getResult();
console.log(result); // 24
```

#### m. Implement Promise Class with Handling of Error Bubbling Upstream
**Explanation:** Custom implementation of the Promise class with error handling.

**Example:**
```javascript
class MyPromise {
    constructor(executor) {
        this.state = 'pending';
        this.value = undefined;
        this.reason = undefined;
        this.onResolvedCallbacks = [];
        this.onRejectedCallbacks = [];
        try {
            executor(this.resolve.bind(this), this.reject.bind(this));
        } catch (error) {
            this.reject(error);


Continuing with the implementation of the custom `Promise` class:

```javascript
        }
    }
    resolve(value) {
        if (this.state === 'pending') {
            this.state = 'fulfilled';
            this.value = value;
            this.onResolvedCallbacks.forEach(fn => fn());
        }
    }
    reject(reason) {
        if (this.state === 'pending') {
            this.state = 'rejected';
            this.reason = reason;
            this.onRejectedCallbacks.forEach(fn => fn());
        }
    }
    then(onFulfilled, onRejected) {
        return new MyPromise((resolve, reject) => {
            if (this.state === 'fulfilled') {
                try {
                    const x = onFulfilled(this.value);
                    resolve(x);
                } catch (error) {
                    reject(error);
                }
            }
            if (this.state === 'rejected') {
                try {
                    const x = onRejected(this.reason);
                    resolve(x);
                } catch (error) {
                    reject(error);
                }
            }
            if (this.state === 'pending') {
                this.onResolvedCallbacks.push(() => {
                    try {
                        const x = onFulfilled(this.value);
                        resolve(x);
                    } catch (error) {
                        reject(error);
                    }
                });
                this.onRejectedCallbacks.push(() => {
                    try {
                        const x = onRejected(this.reason);
                        resolve(x);
                    } catch (error) {
                        reject(error);
                    }
                });
            }
        });
    }

    catch(onRejected) {
        return this.then(null, onRejected);
    }
}

// Example usage:
const promise = new MyPromise((resolve, reject) => {
    setTimeout(() => resolve('Success!'), 1000);
});

promise
    .then(result => {
        console.log(result); // 'Success!'
        return result + ' Again!';
    })
    .then(result => {
        console.log(result); // 'Success! Again!'
    })
    .catch(error => {
        console.error(error);
    });
```

#### n. Polyfill for `JSON.stringify`
**Explanation:** Implement a function to convert JavaScript objects to JSON strings.

**Example:**
```javascript
function jsonStringify(obj) {
    if (typeof obj === 'string') return `"${obj}"`;
    if (typeof obj === 'number' || typeof obj === 'boolean') return String(obj);
    if (obj === null) return 'null';
    if (Array.isArray(obj)) {
        return '[' + obj.map(jsonStringify).join(',') + ']';
    }
    if (typeof obj === 'object') {
        const keys = Object.keys(obj);
        return '{' + keys.map(key => `"${key}":${jsonStringify(obj[key])}`).join(',') + '}';
    }
}

// Example usage:
const obj = { a: 1, b: 'test', c: [1, 2, 3] };
console.log(jsonStringify(obj)); // '{"a":1,"b":"test","c":[1,2,3]}'
```

#### o. Implement Lodash Polyfill `groupBy`
**Explanation:** Create a function to group array items by a specified criterion.

**Example:**
```javascript
function groupBy(array, fn) {
    return array.reduce((result, item) => {
        const key = fn(item);
        if (!result[key]) {
            result[key] = [];
        }
        result[key].push(item);
        return result;
    }, {});
}

// Example usage:
const numbers = [6.1, 4.2, 6.3];
const grouped = groupBy(numbers, Math.floor);
console.log(grouped); // { '4': [4.2], '6': [6.1, 6.3] }
```

These explanations and examples should help you prepare for your interviews with a solid understanding of these advanced JavaScript concepts. If you need further clarification or more examples, feel free to ask!
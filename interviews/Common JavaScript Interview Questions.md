### Detailed Answers for Common JavaScript Interview Questions

#### a. Lexical Scoping
Lexical scoping means that the scope of a variable is determined by its position in the source code. Variables defined inside a function are not accessible outside that function. 

**Example:**
```javascript
function outer() {
    var outerVar = 'I am outside!';
    function inner() {
        var innerVar = 'I am inside!';
        console.log(outerVar); // Accessible
    }
    console.log(innerVar); // Error: innerVar is not defined
    inner();
}
outer();
```

#### b. Hoisting, Temporal Dead Zone
Hoisting is JavaScript's default behavior of moving declarations to the top of the scope. The Temporal Dead Zone (TDZ) is the period between the entering of the scope and the point where the variable is declared and initialized.

**Example:**
```javascript
console.log(a); // undefined due to hoisting
var a = 5;

console.log(b); // ReferenceError due to TDZ
let b = 10;
```

#### c. Closure
A closure is a function that has access to its own scope, the outer function's scope, and the global scope. 

**Example:**
```javascript
function outerFunction(outerVariable) {
    return function innerFunction(innerVariable) {
        console.log('Outer Variable:', outerVariable);
        console.log('Inner Variable:', innerVariable);
    };
}
const newFunction = outerFunction('outside');
newFunction('inside');
```

#### d. ES6 Features
**let, const, and var:** `let` and `const` are block-scoped, `var` is function-scoped.
**Template Literals:** Allow embedded expressions using backticks.
**Destructuring:** Extracts properties from objects/arrays.
**Promises:** Handle asynchronous operations.
**Classes:** Syntactic sugar over JavaScript’s prototype-based inheritance.
**Modules:** Allow import/export of code between files.

**Examples:**
```javascript
// let, const, var
let a = 10;
const b = 20;
var c = 30;

// Template Literals
const name = 'John';
console.log(`Hello, ${name}!`);

// Destructuring
const obj = { x: 1, y: 2 };
const { x, y } = obj;

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
const person = new Person('John');
person.greet();

// Modules (in separate files)
// export const greet = () => 'Hello';
// import { greet } from './greet.js';
```

#### e. Is JavaScript Asynchronous Language?
JavaScript is single-threaded and synchronous by default but can be asynchronous using callbacks, promises, async/await, and events.

#### f. Events in JS? Event Bubbling and Capturing?
Events are actions that occur when a user interacts with a web page. Event bubbling and capturing are two phases of event propagation. Bubbling starts from the target element and propagates up, while capturing starts from the root and propagates down.

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
**Web Worker:** Runs scripts in background threads, enhancing performance.
**Service Worker:** Acts as a proxy between the web app and the network, allowing for features like offline support and background sync.

#### h. Write a Memoization Function
Memoization is an optimization technique to speed up function calls by storing the results of expensive function calls and returning the cached result when the same inputs occur again.

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

#### i. ‘this’ in JS
`this` refers to the object that is executing the current function. In the global context, `this` refers to the global object (window in browsers). In a method, `this` refers to the object. In a constructor, `this` refers to the newly created instance.

#### j. Prototype and Prototypal Inheritance
Every JavaScript object has a prototype, which is also an object. Objects inherit properties and methods from their prototype.

**Example:**
```javascript
function Person(name) {
    this.name = name;
}
Person.prototype.greet = function() {
    console.log(`Hello, ${this.name}!`);
};
const person = new Person('John');
person.greet(); // Hello, John!
```

#### k. How Browsers Work When You Hit on a URL?
1. URL is parsed.
2. DNS lookup to find the IP address.
3. TCP connection is established.
4. HTTP request is sent to the server.
5. Server processes the request and sends back a response.
6. Browser renders the content.

#### l. Local Storage vs Session Storage vs Cookies
**Local Storage:** Stores data with no expiration date.
**Session Storage:** Stores data for the duration of the page session.
**Cookies:** Store data with an expiration date, sent to the server with every HTTP request.

#### m. Web APIs like setTimeout & setInterval
`setTimeout` and `setInterval` are Web APIs that schedule tasks to run after a delay or repeatedly at specified intervals.

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
Infinite scroll is a web design technique that loads more content as the user scrolls down the page, creating an endless scrolling experience.

**Example:**
```javascript
window.addEventListener('scroll', () => {
    if (window.innerHeight + window.scrollY >= document.body.offsetHeight) {
        // Load more content
    }
});
```

These answers provide a detailed understanding of common JavaScript interview questions, complete with practical examples. If you need further clarification on any topic, feel free to ask!
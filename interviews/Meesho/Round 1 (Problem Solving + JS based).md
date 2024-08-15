Sure! Let's break down each part of the interview questions and provide detailed explanations with practical use cases and code examples.

### Round 1 (Problem Solving + JS based):

#### 1. Polyfill for Lodash GroupBy Function

The `groupBy` function in Lodash creates an object composed of keys generated from the results of running each element of a collection through an iteratee function. Here’s a polyfill for it:

```javascript
function groupBy(collection, iteratee) {
    return collection.reduce((result, item) => {
        // Determine the key
        const key = typeof iteratee === 'function' ? iteratee(item) : item[iteratee];
        // Initialize the key if it doesn't exist
        if (!result[key]) {
            result[key] = [];
        }
        // Push the item into the appropriate group
        result[key].push(item);
        return result;
    }, {});
}

// Example usage:
const data = [
    { category: 'fruit', name: 'apple' },
    { category: 'fruit', name: 'banana' },
    { category: 'vegetable', name: 'carrot' },
    { category: 'vegetable', name: 'lettuce' }
];

console.log(groupBy(data, 'category'));
// Output:
// {
//   fruit: [{ category: 'fruit', name: 'apple' }, { category: 'fruit', name: 'banana' }],
//   vegetable: [{ category: 'vegetable', name: 'carrot' }, { category: 'vegetable', name: 'lettuce' }]
// }
```

#### 2. Explain About Service Workers

A **service worker** is a script that runs in the background, separate from a web page, and provides features like:

- **Offline support:** Using service workers and caching, a website can function even when there is no network connection.
- **Push notifications:** Service workers enable the web application to receive push notifications.
- **Background sync:** They can synchronize data in the background when the user has connectivity.

##### Key Features:
- Runs separately from the main browser thread.
- Doesn’t have direct access to the DOM.
- Provides a programmable network proxy.
- Can intercept network requests and decide what to do with them (serve from cache, fetch from network, etc.).

##### Example:
```javascript
// Registering a service worker
if ('serviceWorker' in navigator) {
    navigator.serviceWorker.register('/service-worker.js')
        .then(function(registration) {
            console.log('Service Worker registered with scope:', registration.scope);
        }).catch(function(error) {
            console.log('Service Worker registration failed:', error);
        });
}

// Inside /service-worker.js
self.addEventListener('install', function(event) {
    // Perform install steps
    event.waitUntil(
        caches.open('my-cache')
            .then(function(cache) {
                return cache.addAll([
                    '/',
                    '/index.html',
                    '/styles.css',
                    '/script.js',
                    '/image.jpg'
                ]);
            })
    );
});

self.addEventListener('fetch', function(event) {
    event.respondWith(
        caches.match(event.request)
            .then(function(response) {
                // Cache hit - return the response
                if (response) {
                    return response;
                }
                return fetch(event.request);
            })
    );
});
```

#### 3. Closures, Call, Apply, Bind, and Hoisting

##### Closures:
A **closure** is a function that retains access to its lexical scope, even when the function is executed outside that scope.

Example:
```javascript
function makeCounter() {
    let count = 0;
    return function() {
        count++;
        return count;
    };
}

const counter = makeCounter();
console.log(counter()); // 1
console.log(counter()); // 2
```

##### Call, Apply, and Bind:
These methods are used to control the `this` context of a function.

- **call:** Invokes a function with a given `this` value and arguments provided individually.
- **apply:** Invokes a function with a given `this` value and arguments provided as an array.
- **bind:** Returns a new function with a given `this` value and initial arguments.

Example:
```javascript
function greet(greeting, punctuation) {
    console.log(`${greeting}, ${this.name}${punctuation}`);
}

const person = { name: 'Alice' };

greet.call(person, 'Hello', '!'); // Hello, Alice!
greet.apply(person, ['Hi', '.']); // Hi, Alice.
const boundGreet = greet.bind(person);
boundGreet('Hey', '!!'); // Hey, Alice!!
```

##### Hoisting:
Hoisting is JavaScript's default behavior of moving declarations to the top of the current scope.

Example:
```javascript
console.log(a); // undefined
var a = 5;

function foo() {
    console.log(b); // undefined
    var b = 10;
}

foo();
```

### Round 2 (Machine coding + Frontend):

#### 1. Convert the Given Component to a Paginated Component

Example of a React component showing a paginated list of images:

```javascript
import React, { useState } from 'react';

const PaginatedImages = ({ images }) => {
    const [currentPage, setCurrentPage] = useState(1);
    const imagesPerPage = 5;

    const indexOfLastImage = currentPage * imagesPerPage;
    const indexOfFirstImage = indexOfLastImage - imagesPerPage;
    const currentImages = images.slice(indexOfFirstImage, indexOfLastImage);

    const paginate = (pageNumber) => setCurrentPage(pageNumber);

    return (
        <div>
            <ul>
                {currentImages.map((image, index) => (
                    <li key={index}><img src={image} alt={`img-${index}`} /></li>
                ))}
            </ul>
            <div>
                {Array.from({ length: Math.ceil(images.length / imagesPerPage) }, (_, index) => (
                    <button key={index} onClick={() => paginate(index + 1)}>
                        {index + 1}
                    </button>
                ))}
            </div>
        </div>
    );
};

export default PaginatedImages;

// Usage:
// const images = [ 'url1', 'url2', 'url3', ..., 'urlN' ];
// <PaginatedImages images={images} />
```

#### 2. Output Based Questions on Promises and setTimeout

##### Promises Example:
```javascript
console.log('start');

const promise1 = new Promise((resolve, reject) => {
  console.log('promise1');
  resolve('resolved1');
});

promise1.then((res) => {
  console.log(res);
});

const promise2 = new Promise((resolve, reject) => {
  console.log('promise2');
  resolve('resolved2');
});

promise2.then((res) => {
  console.log(res);
});

console.log('end');

// Output:
// start
// promise1
// promise2
// end
// resolved1
// resolved2
```

##### setTimeout Example:
```javascript
console.log('start');

setTimeout(() => {
  console.log('timeout1');
}, 0);

setTimeout(() => {
  console.log('timeout2');
}, 0);

Promise.resolve().then(() => {
  console.log('promise1');
}).then(() => {
  console.log('promise2');
});

console.log('end');

// Output:
// start
// end
// promise1
// promise2
// timeout1
// timeout2
```

#### 3. Theoretical Questions on Types of Storages, Variables in JS, JWT, etc.

##### Types of Storages:
- **LocalStorage:** Stores data with no expiration date. Data is persisted even after the browser is closed.
- **SessionStorage:** Stores data for the duration of the page session. Data is cleared when the page session ends.
- **Cookies:** Data stored in the form of key-value pairs that can be set to expire after a certain time. Sent with every HTTP request.

##### Variables in JS:
- **var:** Function-scoped, hoisted to the top of the function.
- **let:** Block-scoped, not hoisted to the top of the block.
- **const:** Block-scoped, not hoisted, must be assigned a value at the time of declaration.

##### JWT (JSON Web Token):
JWT is a compact, URL-safe means of representing claims to be transferred between two parties. It is commonly used for authentication and authorization.

Example:
```javascript
// Encoding a JWT
const jwt = require('jsonwebtoken');
const token = jwt.sign({ username: 'user1' }, 'secretKey', { expiresIn: '1h' });

// Decoding a JWT
try {
    const decoded = jwt.verify(token, 'secretKey');
    console.log(decoded.username); // 'user1'
} catch (err) {
    console.log('Invalid token');
}
```

These explanations and examples cover the core concepts and practical implementations for the given questions.
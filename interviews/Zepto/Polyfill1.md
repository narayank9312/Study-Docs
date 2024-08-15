Let's delve into the advanced JavaScript concepts, including writing polyfills for `bind`, `call`, and `apply` methods, and solve two problem-solving questions.

### Polyfill for `Function.prototype.bind`

The `bind` method creates a new function that, when called, has its `this` keyword set to the provided value, with a given sequence of arguments preceding any provided when the new function is called.

Here’s how you can create a polyfill for `bind`:

```javascript
if (!Function.prototype.bind) {
  Function.prototype.bind = function(context, ...args) {
    if (typeof this !== 'function') {
      throw new TypeError('Function.prototype.bind - what is trying to be bound is not callable');
    }

    const self = this;

    return function(...newArgs) {
      return self.apply(context, args.concat(newArgs));
    };
  };
}
```

### Polyfill for `Function.prototype.call`

The `call` method calls a function with a given `this` value and arguments provided individually.

Here’s how you can create a polyfill for `call`:

```javascript
if (!Function.prototype.call) {
  Function.prototype.call = function(context, ...args) {
    context = context || window;
    const uniqueSym = Symbol();
    context[uniqueSym] = this;
    
    const result = context[uniqueSym](...args);
    delete context[uniqueSym];
    
    return result;
  };
}
```

### Polyfill for `Function.prototype.apply`

The `apply` method calls a function with a given `this` value, and arguments provided as an array (or an array-like object).

Here’s how you can create a polyfill for `apply`:

```javascript
if (!Function.prototype.apply) {
  Function.prototype.apply = function(context, args) {
    context = context || window;
    const uniqueSym = Symbol();
    context[uniqueSym] = this;
    
    let result;
    if (!args) {
      result = context[uniqueSym]();
    } else {
      result = context[uniqueSym](...args);
    }
    delete context[uniqueSym];
    
    return result;
  };
}
```

### Problem-Solving Questions

#### 1. Flatten a Nested Object

Given a nested object, flatten it into a single level object where the keys are paths in the original object.

Example:
```javascript
const nestedObj = {
  a: {
    b: {
      c: 1,
      d: 2
    },
    e: 3
  },
  f: 4
};

const flattenObject = (obj, parentKey = '', res = {}) => {
  for (let key in obj) {
    if (obj.hasOwnProperty(key)) {
      const propKey = parentKey ? `${parentKey}.${key}` : key;
      if (typeof obj[key] === 'object' && obj[key] !== null && !Array.isArray(obj[key])) {
        flattenObject(obj[key], propKey, res);
      } else {
        res[propKey] = obj[key];
      }
    }
  }
  return res;
};

const flatObj = flattenObject(nestedObj);
console.log(flatObj); // { 'a.b.c': 1, 'a.b.d': 2, 'a.e': 3, 'f': 4 }
```

#### 2. Deep Clone an Object

Write a function to deep clone an object, ensuring all nested objects and arrays are also cloned.

Example:
```javascript
const deepClone = (obj) => {
  if (obj === null || typeof obj !== 'object') {
    return obj;
  }
  
  if (Array.isArray(obj)) {
    const arrCopy = [];
    for (let i = 0; i < obj.length; i++) {
      arrCopy[i] = deepClone(obj[i]);
    }
    return arrCopy;
  }
  
  const objCopy = {};
  for (let key in obj) {
    if (obj.hasOwnProperty(key)) {
      objCopy[key] = deepClone(obj[key]);
    }
  }
  return objCopy;
};

const originalObj = {
  a: 1,
  b: {
    c: 2,
    d: [3, 4, 5],
    e: {
      f: 6
    }
  }
};

const clonedObj = deepClone(originalObj);
console.log(clonedObj); // { a: 1, b: { c: 2, d: [3, 4, 5], e: { f: 6 } } }
```

### Advanced JavaScript Concepts

#### Closures

A closure is a function that has access to its own scope, the scope of the outer function, and the global scope.

Example:
```javascript
function outerFunction(outerVariable) {
  return function innerFunction(innerVariable) {
    console.log('Outer Variable: ' + outerVariable);
    console.log('Inner Variable: ' + innerVariable);
  };
}

const newFunction = outerFunction('outside');
newFunction('inside');
// Output:
// Outer Variable: outside
// Inner Variable: inside
```

#### Execution Context and Scope

Each time a function is invoked, a new execution context is created. The execution context is composed of:
- Variable Object (VO)
- Scope Chain
- `this` value

Example:
```javascript
var a = 10;

function outer() {
  var b = 20;

  function inner() {
    var c = 30;
    console.log(a, b, c); // 10 20 30
  }

  inner();
}

outer();
```

#### Hoisting

JavaScript Hoisting refers to the process where the interpreter moves variable and function declarations to the top of their containing scope before execution.

Example:
```javascript
console.log(foo); // undefined
var foo = 'bar';
```

#### let, const, var

- **`var`**:
  - Function-scoped.
  - Hoisted to the top of its scope and initialized with `undefined`.
  - Can be re-declared and updated.

- **`let`**:
  - Block-scoped.
  - Hoisted but not initialized, leading to TDZ.
  - Cannot be re-declared within the same scope but can be updated.

- **`const`**:
  - Block-scoped.
  - Hoisted but not initialized, leading to TDZ.
  - Cannot be re-declared or updated within the same scope.
  - Must be initialized at the time of declaration.

Example:
```javascript
// var
var x = 1;
console.log(x); // 1
x = 2;
console.log(x); // 2
var x = 3;
console.log(x); // 3

// let
let y = 1;
console.log(y); // 1
y = 2;
console.log(y); // 2
// let y = 3; // SyntaxError: Identifier 'y' has already been declared

// const
const z = 1;
console.log(z); // 1
// z = 2; // TypeError: Assignment to constant variable.
```

By understanding these concepts and practicing polyfills and problem-solving questions, you will be well-prepared for JavaScript technical interviews.
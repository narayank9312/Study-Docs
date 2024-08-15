Sure, let's start with some examples and explanations for each of these:

### Polyfills

A polyfill is a piece of code (usually JavaScript on the Web) used to provide modern functionality on older browsers that do not natively support it.

#### Polyfill for `Array.prototype.reduce`

Here's how you can write a polyfill for `Array.prototype.reduce`:

```javascript
if (!Array.prototype.reduce) {
  Array.prototype.reduce = function(callback, initialValue) {
    if (this == null) {
      throw new TypeError('Array.prototype.reduce called on null or undefined');
    }
    if (typeof callback !== 'function') {
      throw new TypeError(callback + ' is not a function');
    }

    let array = Object(this);
    let length = array.length >>> 0;
    let accumulator = initialValue;
    let startIndex = 0;

    if (arguments.length < 2) {
      while (startIndex < length && !(startIndex in array)) {
        startIndex++;
      }
      if (startIndex >= length) {
        throw new TypeError('Reduce of empty array with no initial value');
      }
      accumulator = array[startIndex++];
    }

    for (let i = startIndex; i < length; i++) {
      if (i in array) {
        accumulator = callback(accumulator, array[i], i, array);
      }
    }
    return accumulator;
  };
}
```

#### Polyfill for `Promise.all`

Here's a polyfill for `Promise.all`:

```javascript
if (!Promise.all) {
  Promise.all = function(promises) {
    return new Promise((resolve, reject) => {
      if (!Array.isArray(promises)) {
        return reject(new TypeError('Promise.all accepts an array'));
      }

      let resolvedCounter = 0;
      const promiseNum = promises.length;
      const resolvedValues = new Array(promiseNum);

      for (let i = 0; i < promiseNum; i++) {
        Promise.resolve(promises[i])
          .then(value => {
            resolvedCounter++;
            resolvedValues[i] = value;
            if (resolvedCounter === promiseNum) {
              resolve(resolvedValues);
            }
          })
          .catch(err => {
            reject(err);
          });
      }
    });
  };
}
```

### Output-Based Questions

These questions require you to determine the output of a piece of code. Here are a few examples:

1. **Example 1:**

```javascript
function test() {
  console.log(a);
  console.log(b);
  var a = 1;
  let b = 2;
}

test();
```

**Output:**

```
undefined
ReferenceError: Cannot access 'b' before initialization
```

Explanation: The variable `a` is hoisted and initialized with `undefined`, but `b` is hoisted in the TDZ (Temporal Dead Zone) and cannot be accessed before initialization.

2. **Example 2:**

```javascript
const x = 10;
const y = '10';

console.log(x == y);
console.log(x === y);
```

**Output:**

```
true
false
```

Explanation: The `==` operator performs type coercion, so `10` (number) and `'10'` (string) are considered equal. The `===` operator checks for both value and type equality, which fails.

### Small Coding Exercise: Flatten an Object

To flatten a nested object, you can recursively iterate over its properties and create a new object with flattened keys.

```javascript
function flattenObject(obj, parentKey = '', res = {}) {
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
}

// Example usage:
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

const flatObj = flattenObject(nestedObj);
console.log(flatObj);
// Output: { 'a.b.c': 1, 'a.b.d': 2, 'a.e': 3, 'f': 4 }
```

### let vs var vs const

#### `var`

- **Scope**: Function-scoped or globally-scoped.
- **Hoisting**: Variables declared with `var` are hoisted to the top of their scope and initialized with `undefined`.
- **Re-declaration and updating**: Can be re-declared and updated within its scope.

Example:
```javascript
function varExample() {
  console.log(x); // undefined
  var x = 10;
  console.log(x); // 10
}
varExample();
```

#### `let`

- **Scope**: Block-scoped (inside curly braces `{}`).
- **Hoisting**: Variables declared with `let` are hoisted to the top of their block but not initialized, leading to the Temporal Dead Zone (TDZ).
- **Re-declaration and updating**: Cannot be re-declared within the same scope but can be updated.

Example:
```javascript
function letExample() {
  // console.log(x); // ReferenceError: Cannot access 'x' before initialization
  let x = 10;
  console.log(x); // 10
}
letExample();
```

#### `const`

- **Scope**: Block-scoped (inside curly braces `{}`).
- **Hoisting**: Variables declared with `const` are hoisted to the top of their block but not initialized, leading to the Temporal Dead Zone (TDZ).
- **Re-declaration and updating**: Cannot be re-declared or updated within the same scope. Must be initialized at the time of declaration.

Example:
```javascript
function constExample() {
  // console.log(x); // ReferenceError: Cannot access 'x' before initialization
  const x = 10;
  console.log(x); // 10
  // x = 20; // TypeError: Assignment to constant variable.
}
constExample();
```

#### Temporal Dead Zone (TDZ)

The TDZ is the time between entering the scope and the declaration of a variable where the variable cannot be accessed.

Example:
```javascript
{
  // console.log(a); // ReferenceError: Cannot access 'a' before initialization
  let a = 10;

  // console.log(b); // ReferenceError: Cannot access 'b' before initialization
  const b = 20;
}
```

These examples and explanations should give you a solid foundation on polyfills, understanding outputs of code snippets, and writing small coding exercises like flattening an object.
Certainly! Let's go into detail on writing a polyfill for `Array.prototype.reduce` and `Promise.all`, then cover object restructuring and the differences between `let`, `const`, and `var`.

### Polyfill for `Array.prototype.reduce`

#### Understanding `Array.prototype.reduce`

The `reduce` method applies a function against an accumulator and each element in the array (from left to right) to reduce it to a single value.

Example:
```javascript
const array = [1, 2, 3, 4];
const sum = array.reduce((accumulator, currentValue) => accumulator + currentValue, 0);
console.log(sum); // 10
```

#### Writing the Polyfill

1. **Check for null or undefined array**: If the array is null or undefined, throw a `TypeError`.
2. **Check if callback is a function**: Throw a `TypeError` if the callback is not a function.
3. **Handle initial value**: Check if an initial value is provided.
4. **Iterate over the array**: Accumulate values using the callback function.

Here's the complete polyfill:

```javascript
if (!Array.prototype.reduce) {
  Array.prototype.reduce = function(callback /*, initialValue*/) {
    if (this == null) {
      throw new TypeError('Array.prototype.reduce called on null or undefined');
    }
    if (typeof callback !== 'function') {
      throw new TypeError(callback + ' is not a function');
    }

    const t = Object(this);
    const len = t.length >>> 0;
    let k = 0;
    let value;

    if (arguments.length > 1) {
      value = arguments[1];
    } else {
      while (k < len && !(k in t)) {
        k++;
      }
      if (k >= len) {
        throw new TypeError('Reduce of empty array with no initial value');
      }
      value = t[k++];
    }

    for (; k < len; k++) {
      if (k in t) {
        value = callback(value, t[k], k, t);
      }
    }
    return value;
  };
}
```

### Polyfill for `Promise.all`

#### Understanding `Promise.all`

`Promise.all` takes an iterable of promises and returns a single Promise that resolves when all the promises have resolved or rejects if any promise is rejected.

Example:
```javascript
const promise1 = Promise.resolve(3);
const promise2 = 42;
const promise3 = new Promise((resolve, reject) => {
  setTimeout(resolve, 100, 'foo');
});

Promise.all([promise1, promise2, promise3]).then(values => {
  console.log(values); // [3, 42, 'foo']
});
```

#### Writing the Polyfill

1. **Check if all elements are promises**: Use `Promise.resolve` to ensure each element is a promise.
2. **Track resolved values and count**: Use an array to store resolved values and a counter to track the number of resolved promises.
3. **Handle rejections**: If any promise rejects, reject the main promise.

Here's the complete polyfill:

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

### Object Restructuring

Object restructuring (or destructuring) allows you to extract properties from an object and assign them to variables.

Example:
```javascript
const user = {
  id: 42,
  isVerified: true
};

const { id, isVerified } = user;

console.log(id); // 42
console.log(isVerified); // true
```

You can also rename variables during destructuring:
```javascript
const user = {
  id: 42,
  isVerified: true
};

const { id: userId, isVerified: userStatus } = user;

console.log(userId); // 42
console.log(userStatus); // true
```

### `let` vs `const` vs `var`

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

These explanations should provide a comprehensive understanding of writing polyfills for `Array.prototype.reduce` and `Promise.all`, object restructuring, and the differences between `let`, `const`, and `var`, including the concept of the Temporal Dead Zone.
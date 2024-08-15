It sounds like you were close to performing well, but perhaps there were some details that needed more precision. Let's go through the code example you provided, the polyfills for `Promise.all` and `Array.prototype.reduce`, and the differences between `Array.filter` and `Array.map`. This will help ensure you have a solid grasp of these topics for future interviews.

### 1. Code Example Explanation

Let's break down the provided code snippet step-by-step:

```javascript
(function() { 
  console.log(a); 
  if (true) { 
    var a = 'a'; 
  } 
  console.log(a); 
  console.log(b); 
  const bar = function() { 
    var b = 'b'; 
    console.log(b); 
  }; 
  bar(); 
  console.log(b); 
})();
```

**Step-by-Step Execution**:

1. **`console.log(a)`**:
   - `a` is declared using `var` within the function scope.
   - `var` declarations are hoisted, but the initialization is not.
   - So, the first `console.log(a)` outputs `undefined`.

2. **`if (true) { var a = 'a'; }`**:
   - The `var a` declaration is hoisted to the top of the function scope.
   - The initialization `a = 'a'` happens only when the `if` condition is true.

3. **`console.log(a)`**:
   - By now, `a` has been assigned the value `'a'`.
   - This `console.log(a)` outputs `'a'`.

4. **`console.log(b)`**:
   - `b` is not declared in the outer function scope, so this throws a `ReferenceError: b is not defined`.

5. **`const bar = function() { var b = 'b'; console.log(b); };`**:
   - `bar` is a function expression assigned to a constant `bar`.
   - Inside `bar`, `b` is declared and assigned `'b'` using `var`.

6. **`bar()`**:
   - Invokes the `bar` function.
   - Inside `bar`, `console.log(b)` outputs `'b'`.

7. **`console.log(b)`**:
   - After the `bar` function has executed, `b` is not defined in the outer function scope.
   - So, this will throw a `ReferenceError: b is not defined`.

### 2. Polyfill for `Promise.all` (pre-ES6)

Here’s a polyfill for `Promise.all` using ES5 syntax:

```javascript
if (typeof Promise === "undefined") {
  Promise = function(executor) {
    var self = this;
    self.state = "pending";
    self.value = undefined;
    self.deferred = [];

    function resolve(value) {
      if (self.state === "pending") {
        self.state = "fulfilled";
        self.value = value;
        self.deferred.forEach(function(handler) {
          handler(value);
        });
      }
    }

    function reject(reason) {
      if (self.state === "pending") {
        self.state = "rejected";
        self.value = reason;
        self.deferred.forEach(function(handler) {
          handler(reason);
        });
      }
    }

    try {
      executor(resolve, reject);
    } catch (error) {
      reject(error);
    }
  };

  Promise.prototype.then = function(onFulfilled, onRejected) {
    var self = this;
    return new Promise(function(resolve, reject) {
      function handle(value) {
        try {
          var result = onFulfilled ? onFulfilled(value) : value;
          resolve(result);
        } catch (error) {
          reject(error);
        }
      }

      if (self.state === "fulfilled") {
        handle(self.value);
      } else {
        self.deferred.push(handle);
      }
    });
  };

  Promise.prototype.catch = function(onRejected) {
    return this.then(null, onRejected);
  };
}

if (!Promise.all) {
  Promise.all = function(promises) {
    return new Promise(function(resolve, reject) {
      if (!Array.isArray(promises)) {
        return reject(new TypeError("Promise.all accepts an array"));
      }

      var resolvedCounter = 0;
      var promiseNum = promises.length;
      var resolvedValues = new Array(promiseNum);

      function processPromise(i, promise) {
        Promise.resolve(promise)
          .then(function(value) {
            resolvedCounter++;
            resolvedValues[i] = value;
            if (resolvedCounter === promiseNum) {
              resolve(resolvedValues);
            }
          })
          .catch(function(reason) {
            reject(reason);
          });
      }

      for (var i = 0; i < promiseNum; i++) {
        processPromise(i, promises[i]);
      }
    });
  };
}
```

### 3. Polyfill for `Array.prototype.reduce`

Here’s a polyfill for `Array.prototype.reduce`:

```javascript
if (!Array.prototype.reduce) {
  Array.prototype.reduce = function(callback, initialValue) {
    if (this == null) {
      throw new TypeError('Array.prototype.reduce called on null or undefined');
    }
    if (typeof callback !== 'function') {
      throw new TypeError(callback + ' is not a function');
    }

    var array = Object(this);
    var length = array.length >>> 0;
    var value;
    var i = 0;

    if (arguments.length >= 2) {
      value = initialValue;
    } else {
      while (i < length && !(i in array)) {
        i++;
      }
      if (i >= length) {
        throw new TypeError('Reduce of empty array with no initial value');
      }
      value = array[i++];
    }

    for (; i < length; i++) {
      if (i in array) {
        value = callback(value, array[i], i, array);
      }
    }

    return value;
  };
}
```

### 4. Difference Between `Array.filter` and `Array.map`

- **`Array.filter`**:
  - Creates a new array with all elements that pass the test implemented by the provided function.
  - Does not modify the original array.
  - Example:
    ```javascript
    const numbers = [1, 2, 3, 4, 5];
    const evens = numbers.filter(num => num % 2 === 0);
    console.log(evens); // [2, 4]
    ```

- **`Array.map`**:
  - Creates a new array with the results of calling a provided function on every element in the calling array.
  - Does not modify the original array.
  - Example:
    ```javascript
    const numbers = [1, 2, 3, 4, 5];
    const doubled = numbers.map(num => num * 2);
    console.log(doubled); // [2, 4, 6, 8, 10]
    ```

### Conclusion

You have a strong foundation in JavaScript, and it's clear that you are familiar with advanced concepts and polyfills. The key to success in technical interviews is precision and clarity. Reviewing these explanations and practicing similar problems will help you solidify your understanding and improve your performance in future interviews.
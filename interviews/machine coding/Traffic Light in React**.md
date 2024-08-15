Let's break down your tasks step by step, starting with the creation of the traffic light system in React.

### 1. **Creating a Configurable Traffic Light in React**

#### **Step 1: Define the Configuration**

We'll start by defining a configuration for the traffic lights. This configuration will specify the order of the lights and the duration each light should stay on.

```javascript
const lightConfig = [
  { color: 'red', duration: 3000 },
  { color: 'yellow', duration: 1000 },
  { color: 'green', duration: 2000 },
];
```

#### **Step 2: Create the Traffic Light Component**

Now, let's create a `TrafficLight` component that will cycle through the lights based on the configuration.

```javascript
import React, { useState, useEffect } from 'react';

const TrafficLight = ({ config }) => {
  const [currentIndex, setCurrentIndex] = useState(0);
  const { color } = config[currentIndex];

  useEffect(() => {
    const timeoutId = setTimeout(() => {
      setCurrentIndex((currentIndex + 1) % config.length);
    }, config[currentIndex].duration);

    return () => clearTimeout(timeoutId);
  }, [currentIndex, config]);

  return (
    <div style={{ width: '100px', height: '300px', backgroundColor: '#333', padding: '10px' }}>
      <div style={{ width: '80px', height: '80px', backgroundColor: color === 'red' ? 'red' : '#222', marginBottom: '10px' }}></div>
      <div style={{ width: '80px', height: '80px', backgroundColor: color === 'yellow' ? 'yellow' : '#222', marginBottom: '10px' }}></div>
      <div style={{ width: '80px', height: '80px', backgroundColor: color === 'green' ? 'green' : '#222', marginBottom: '10px' }}></div>
    </div>
  );
};

function App() {
  return (
    <div className="App">
      <TrafficLight config={lightConfig} />
    </div>
  );
}

export default App;
```

### **Explanation:**
1. **Configuration**: We have a configuration array `lightConfig` that defines the order and duration of each light.
2. **State Management**: We use `useState` to track the current light index.
3. **Effect Hook**: `useEffect` is used to set up a timer based on the current light's duration. When the timer expires, the next light is activated.

### 2. **Output Based Questions**

#### **a. `var`, `let`, `const`, and Hoisting**

```javascript
function example() {
  console.log(foo); // undefined (due to hoisting)
  var foo = 10;
  console.log(foo); // 10

  if (true) {
    let bar = 20;
    console.log(bar); // 20
  }

  // console.log(bar); // ReferenceError: bar is not defined

  const baz = 30;
  // baz = 40; // TypeError: Assignment to constant variable.
}

example();
```

**Explanation:**
- `var` is hoisted and initialized with `undefined`.
- `let` and `const` are hoisted but not initialized, causing a `ReferenceError` if accessed before initialization.
- `const` cannot be reassigned after its initial value is set.

#### **b. Event Loop (Call Stack, Timeouts, Promises, requestAnimationFrame)**

```javascript
console.log('Start');

setTimeout(() => {
  console.log('Timeout');
}, 0);

Promise.resolve().then(() => {
  console.log('Promise');
});

requestAnimationFrame(() => {
  console.log('Animation Frame');
});

console.log('End');
```

**Expected Output:**
```
Start
End
Promise
Animation Frame
Timeout
```

**Explanation:**
- **Call Stack**: Synchronous code is executed first (`Start`, `End`).
- **Microtask Queue**: Promises (`Promise`) are resolved before the next render cycle.
- **Task Queue**: `setTimeout` executes after all microtasks.
- **requestAnimationFrame**: Executes before the next repaint.

#### **c. Closures and Lexical Scoping**

```javascript
function outer() {
  const outerVar = 'I am outer';

  return function inner() {
    const innerVar = 'I am inner';
    console.log(outerVar); // Accessing outer function variable
    console.log(innerVar); // Accessing inner function variable
  };
}

const innerFunc = outer();
innerFunc();
```

**Expected Output:**
```
I am outer
I am inner
```

**Explanation:**
- **Closures**: Inner function retains access to the variables of its outer function even after the outer function has finished execution.
- **Lexical Scoping**: Variables are resolved in the scope in which they were defined, not where they are executed. 

This should cover all your requirements, both in React and JavaScript concepts. Let me know if you need further details!
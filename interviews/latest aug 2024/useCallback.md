### 1. **What is `useCallback`?**
   - `useCallback` is a React Hook that returns a memoized version of a callback function that only changes if one of its dependencies has changed.
   - It's used to prevent unnecessary re-creation of functions during re-renders, which can help optimize performance, especially when passing callbacks to child components.

   **Example**:

   ```javascript
   import React, { useState, useCallback } from 'react';

   function MyComponent() {
       const [count, setCount] = useState(0);

       const increment = useCallback(() => {
           setCount(count + 1);
       }, [count]);

       return (
           <div>
               <p>Count: {count}</p>
               <button onClick={increment}>Increment</button>
           </div>
       );
   }
   ```

   - In this example, the `increment` function will only be re-created if the `count` value changes.

### 2. **What is Redux?**
   - **Redux** is a state management library for JavaScript applications, most commonly used with React.
   - It helps manage the application's state in a single, centralized store, allowing predictable state transitions through actions and reducers.

   **Key Concepts**:
   - **Store**: The single source of truth where the application's state is stored.
   - **Actions**: Plain JavaScript objects that describe what happened in the app (e.g., `{ type: 'INCREMENT' }`).
   - **Reducers**: Functions that take the current state and an action, and return a new state.
   - **Dispatch**: The method used to send actions to the store.

   **Example**:

   ```javascript
   // Action
   const increment = () => ({ type: 'INCREMENT' });

   // Reducer
   const counter = (state = 0, action) => {
       switch (action.type) {
           case 'INCREMENT':
               return state + 1;
           default:
               return state;
       }
   };

   // Store
   const store = createStore(counter);

   store.dispatch(increment()); // State becomes 1
   console.log(store.getState()); // 1
   ```

### 3. **Custom Hook for Timer Operations**

   A custom hook can manage a timer with start, stop, reset, and pause functionalities.

   **Example**:

   ```javascript
   import { useState, useRef } from 'react';

   function useTimer() {
       const [time, setTime] = useState(0);
       const [isRunning, setIsRunning] = useState(false);
       const timerRef = useRef(null);

       const start = () => {
           if (!isRunning) {
               setIsRunning(true);
               timerRef.current = setInterval(() => {
                   setTime(prevTime => prevTime + 1);
               }, 1000);
           }
       };

       const pause = () => {
           clearInterval(timerRef.current);
           setIsRunning(false);
       };

       const reset = () => {
           clearInterval(timerRef.current);
           setIsRunning(false);
           setTime(0);
       };

       const stop = () => {
           clearInterval(timerRef.current);
           setIsRunning(false);
           setTime(0);
       };

       return { time, isRunning, start, pause, reset, stop };
   }

   export default useTimer;
   ```

   - **Usage**:

   ```javascript
   function TimerComponent() {
       const { time, start, pause, reset, stop } = useTimer();

       return (
           <div>
               <p>Time: {time}s</p>
               <button onClick={start}>Start</button>
               <button onClick={pause}>Pause</button>
               <button onClick={reset}>Reset</button>
               <button onClick={stop}>Stop</button>
           </div>
       );
   }
   ```

### 4. **What is `useMemo`?**
   - `useMemo` is a React Hook that returns a memoized value, which is recalculated only when one of its dependencies changes.
   - It's used to optimize performance by avoiding expensive calculations on every render.

   **Example**:

   ```javascript
   import React, { useState, useMemo } from 'react';

   function MyComponent() {
       const [count, setCount] = useState(0);
       const [input, setInput] = useState('');

       const expensiveCalculation = (num) => {
           console.log('Calculating...');
           return num * 2;
       };

       const result = useMemo(() => expensiveCalculation(count), [count]);

       return (
           <div>
               <p>Result: {result}</p>
               <button onClick={() => setCount(count + 1)}>Increment</button>
               <input value={input} onChange={(e) => setInput(e.target.value)} />
           </div>
       );
   }
   ```

   - The `expensiveCalculation` will only be re-run if the `count` changes, not if `input` changes.

### 5. **What Does the `reduce` Function Do in JavaScript?**
   - The `reduce` function in JavaScript is an array method that applies a function against an accumulator and each element in the array (from left to right) to reduce it to a single value.

   **Syntax**:

   ```javascript
   array.reduce((accumulator, currentValue, currentIndex, array) => {
       // return the updated accumulator
   }, initialValue);
   ```

   **Example**:

   ```javascript
   const numbers = [1, 2, 3, 4, 5];

   const sum = numbers.reduce((acc, curr) => acc + curr, 0);

   console.log(sum); // 15
   ```

   - In this example, the `reduce` function sums up all the numbers in the array, starting from the initial value `0`.
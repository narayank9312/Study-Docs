### Understanding `useMemo` and `useCallback` in React

React provides hooks like `useMemo` and `useCallback` to optimize performance by memoizing values and functions. Let's explore these hooks with examples.

#### `useMemo`
The `useMemo` hook is used to memoize the result of a function, preventing it from being recalculated on every render. It takes two arguments: a function that returns a value, and an array of dependencies. If none of the dependencies change between renders, the memoized value is returned.

**Example:**

```jsx
import React, { useMemo, useState } from 'react';

const App = () => {
  const [count, setCount] = useState(0);
  const [dark, setDark] = useState(false);

  const doubleCount = useMemo(() => {
    console.log('Calculating double count...');
    return count * 2;
  }, [count]);

  const themeStyles = useMemo(() => {
    return {
      backgroundColor: dark ? 'black' : 'white',
      color: dark ? 'white' : 'black',
    };
  }, [dark]);

  return (
    <div style={themeStyles}>
      <input 
        type="number" 
        value={count} 
        onChange={(e) => setCount(parseInt(e.target.value))} 
      />
      <button onClick={() => setDark(prevDark => !prevDark)}>Toggle Theme</button>
      <div>Double Count: {doubleCount}</div>
    </div>
  );
};

export default App;
```

In this example, the `doubleCount` value is only recalculated when `count` changes. The `themeStyles` object is only recreated when `dark` changes, preventing unnecessary renders and improving performance.

#### `useCallback`
The `useCallback` hook is used to memoize a function, preventing it from being recreated on every render. It takes two arguments: the function to memoize, and an array of dependencies. If none of the dependencies change between renders, the memoized function is returned.

**Example:**

```jsx
import React, { useCallback, useState } from 'react';

const List = React.memo(({ getItems }) => {
  const [items, setItems] = useState([]);

  React.useEffect(() => {
    setItems(getItems());
    console.log('Updating items...');
  }, [getItems]);

  return (
    <ul>
      {items.map((item, index) => (
        <li key={index}>{item}</li>
      ))}
    </ul>
  );
});

const App = () => {
  const [number, setNumber] = useState(1);
  const [dark, setDark] = useState(false);

  const getItems = useCallback(() => {
    return [number, number + 1, number + 2];
  }, [number]);

  const themeStyles = {
    backgroundColor: dark ? 'black' : 'white',
    color: dark ? 'white' : 'black',
  };

  return (
    <div style={themeStyles}>
      <input 
        type="number" 
        value={number} 
        onChange={(e) => setNumber(parseInt(e.target.value))} 
      />
      <button onClick={() => setDark(prevDark => !prevDark)}>Toggle Theme</button>
      <List getItems={getItems} />
    </div>
  );
};

export default App;
```

In this example, the `getItems` function is only recreated when `number` changes. This prevents the `List` component from re-rendering unnecessarily when the `dark` state changes, improving performance.

### When to Use `useMemo` and `useCallback`
- **useMemo**: Use when you have expensive computations that you want to avoid re-calculating on every render.
- **useCallback**: Use when you want to memoize callback functions, especially when passing them as props to child components to avoid unnecessary re-renders.

### Summary
- `useMemo` and `useCallback` are hooks for optimizing performance by memoizing values and functions.
- Use `useMemo` for memoizing the results of expensive calculations.
- Use `useCallback` for memoizing callback functions to prevent unnecessary re-renders of child components.

By using these hooks appropriately, you can make your React applications more efficient and performant.
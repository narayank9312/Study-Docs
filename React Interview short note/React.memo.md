### React.memo

**Concept**: `React.memo` is a higher-order component that memoizes a functional component, preventing unnecessary re-renders if the component’s props have not changed.

### Example:

**Without React.memo**:
```javascript
import React, { useState } from 'react';

const Child = ({ name }) => {
  console.log('Child component re-rendered');
  return <div>Hello, {name}!</div>;
};

const Parent = () => {
  const [count, setCount] = useState(0);
  return (
    <div>
      <Child name="Alice" />
      <button onClick={() => setCount(count + 1)}>Increment {count}</button>
    </div>
  );
};

export default Parent;
```
- **Issue**: `Child` component re-renders every time the `Parent` component re-renders, even if `name` prop hasn't changed.

**With React.memo**:
```javascript
import React, { useState, memo } from 'react';

const Child = memo(({ name }) => {
  console.log('Child component re-rendered');
  return <div>Hello, {name}!</div>;
});

const Parent = () => {
  const [count, setCount] = useState(0);
  return (
    <div>
      <Child name="Alice" />
      <button onClick={() => setCount(count + 1)}>Increment {count}</button>
    </div>
  );
};

export default Parent;
```
- **Solution**: `Child` component is wrapped in `React.memo`, preventing it from re-rendering if `name` prop doesn't change.

### Explanation:

- **`React.memo`**: Checks if props have changed. If not, it skips re-rendering the component.
- **Use Case**: Improves performance by reducing unnecessary renders.

### Benefits:

1. **Performance Optimization**: Avoids unnecessary re-renders.
2. **Simple to Use**: Wrap the component with `React.memo`.

### Summary:

- **Without `React.memo`**: Child re-renders on every parent re-render.
- **With `React.memo`**: Child re-renders only when props change.

Using `React.memo` is a simple yet effective way to optimize functional components in React.
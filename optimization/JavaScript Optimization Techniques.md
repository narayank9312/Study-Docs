### JavaScript Optimization Techniques

1. **Minimize DOM Manipulations**:
   - Use Document Fragments or innerHTML for batch updates.
   - Minimize direct DOM access.

2. **Debounce and Throttle**:
   - Debouncing delays execution until the activity stops.
   - Throttling limits the frequency of function execution.

3. **Memoization**:
   - Cache results of expensive function calls.
   - Useful in functions with repetitive calculations.

4. **Lazy Loading**:
   - Load resources only when needed.
   - Use IntersectionObserver for images and components.

5. **Code Splitting**:
   - Split code into smaller chunks.
   - Use dynamic imports in frameworks like React.

6. **Optimize Loops**:
   - Minimize the work inside loops.
   - Use `map`, `filter`, `reduce` for functional approaches.

7. **Asynchronous Programming**:
   - Use Promises, `async/await` for non-blocking operations.
   - Optimize network requests with caching and batching.

8. **Reduce Repaints and Reflows**:
   - Minimize style changes and complex layout calculations.

9. **Use Efficient Data Structures**:
   - Choose appropriate data structures like Sets, Maps for optimal performance.

10. **Optimize Event Handling**:
    - Use event delegation for handling multiple similar events.
    - Avoid unnecessary event listeners.

### Example: Debouncing
```javascript
function debounce(func, wait) {
  let timeout;
  return function(...args) {
    clearTimeout(timeout);
    timeout = setTimeout(() => func.apply(this, args), wait);
  };
}

const handleResize = debounce(() => {
  console.log('Resized');
}, 200);

window.addEventListener('resize', handleResize);
```

### Example: Memoization
```javascript
function memoize(fn) {
  const cache = {};
  return function(...args) {
    const key = JSON.stringify(args);
    if (cache[key]) return cache[key];
    const result = fn(...args);
    cache[key] = result;
    return result;
  };
}

const factorial = memoize((n) => {
  if (n <= 1) return 1;
  return n * factorial(n - 1);
});

console.log(factorial(5)); // 120
```

These techniques help improve the performance and responsiveness of JavaScript applications.

### JavaScript Optimization Techniques in React

#### 1. Minimize DOM Manipulations
Use hooks like `useState` and `useEffect` to manage state efficiently and avoid unnecessary DOM manipulations.

```javascript
const ExampleComponent = () => {
  const [data, setData] = useState(null);

  useEffect(() => {
    fetchData().then(setData);
  }, []);
  
  return <div>{data}</div>;
};
```

#### 2. Debounce and Throttle
Debounce and throttle functions to manage frequent updates, such as handling window resize events.

**Debounce Example**:
```javascript
const debounce = (func, delay) => {
  let debounceTimer;
  return (...args) => {
    clearTimeout(debounceTimer);
    debounceTimer = setTimeout(() => func.apply(this, args), delay);
  };
};

const handleInputChange = debounce((value) => {
  console.log('Input changed:', value);
}, 300);
```

**Throttle Example**:
```javascript
const throttle = (func, limit) => {
  let inThrottle;
  return function() {
    const args = arguments;
    const context = this;
    if (!inThrottle) {
      func.apply(context, args);
      inThrottle = true;
      setTimeout(() => inThrottle = false, limit);
    }
  }
};

const handleScroll = throttle(() => {
  console.log('Scrolled!');
}, 1000);

window.addEventListener('scroll', handleScroll);
```

#### 3. Memoization
Use `useMemo` to memoize expensive calculations and `React.memo` to prevent unnecessary re-renders.

**useMemo Example**:
```javascript
const ExpensiveComponent = ({ items }) => {
  const expensiveCalculation = useMemo(() => {
    return items.reduce((sum, item) => sum + item.value, 0);
  }, [items]);

  return <div>Total: {expensiveCalculation}</div>;
};
```

**React.memo Example**:
```javascript
const ChildComponent = React.memo(({ data }) => {
  console.log('ChildComponent rendered');
  return <div>{data}</div>;
});
```

#### 4. Lazy Loading
Use `React.lazy` and `Suspense` to load components only when needed.

```javascript
const LazyComponent = React.lazy(() => import('./LazyComponent'));

const App = () => (
  <Suspense fallback={<div>Loading...</div>}>
    <LazyComponent />
  </Suspense>
);
```

#### 5. Code Splitting
Split code to load only what's needed.

```javascript
const OtherComponent = React.lazy(() => import('./OtherComponent'));

const App = () => (
  <Suspense fallback={<div>Loading...</div>}>
    <OtherComponent />
  </Suspense>
);
```

#### 6. Optimize Loops
Use array methods efficiently.

```javascript
const OptimizedComponent = ({ items }) => {
  return (
    <ul>
      {items.map(item => (
        <li key={item.id}>{item.name}</li>
      ))}
    </ul>
  );
};
```

#### 7. Asynchronous Programming
Use `useEffect` with async functions for non-blocking operations.

```javascript
useEffect(() => {
  const fetchData = async () => {
    const response = await fetch('https://api.example.com/data');
    const data = await response.json();
    setData(data);
  };
  fetchData();
}, []);
```

#### 8. Reduce Repaints and Reflows
Batch updates to state to avoid multiple renders.

```javascript
const [state, setState] = useState({ count: 0, name: '' });

const updateState = () => {
  setState(prevState => ({ ...prevState, count: prevState.count + 1, name: 'John' }));
};
```

#### 9. Use Efficient Data Structures
Use appropriate data structures for performance optimization.

```javascript
const dataMap = new Map();
dataMap.set('key1', 'value1');
dataMap.set('key2', 'value2');
```

#### 10. Optimize Event Handling
Use event delegation and avoid unnecessary event listeners.

```javascript
const handleClick = (event) => {
  if (event.target.matches('.button-class')) {
    console.log('Button clicked');
  }
};

document.addEventListener('click', handleClick);
```

These optimization techniques help improve the performance and efficiency of React applications, ensuring a better user experience.
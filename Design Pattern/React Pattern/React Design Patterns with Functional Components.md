### React Design Patterns with Functional Components

1. **Presentational and Container Components**:
   - **Use Case**: Separation of concerns between UI and logic.
   - **Example**:
     ```javascript
     // Presentational Component
     const UserList = ({ users }) => (
       <ul>
         {users.map(user => <li key={user.id}>{user.name}</li>)}
       </ul>
     );

     // Container Component
     const UserListContainer = () => {
       const [users, setUsers] = useState([]);

       useEffect(() => {
         fetch('/api/users')
           .then(response => response.json())
           .then(data => setUsers(data));
       }, []);

       return <UserList users={users} />;
     };
     ```

2. **Higher-Order Components (HOC)**:
   - **Use Case**: Reuse component logic.
   - **Example**:
     ```javascript
     const withLoading = Component => {
       return function WithLoadingComponent(props) {
         const [loading, setLoading] = useState(true);

         useEffect(() => {
           setLoading(false);
         }, []);

         return loading ? <div>Loading...</div> : <Component {...props} />;
       };
     };

     const UserListWithLoading = withLoading(UserList);
     ```

3. **Render Props**:
   - **Use Case**: Share logic between components using a prop that is a function.
   - **Example**:
     ```javascript
     const MouseTracker = ({ render }) => {
       const [position, setPosition] = useState({ x: 0, y: 0 });

       const handleMouseMove = (event) => {
         setPosition({ x: event.clientX, y: event.clientY });
       };

       return (
         <div onMouseMove={handleMouseMove}>
           {render(position)}
         </div>
       );
     };

     const App = () => (
       <MouseTracker render={({ x, y }) => (
         <h1>The mouse position is ({x}, {y})</h1>
       )} />
     );
     ```

4. **Custom Hooks**:
   - **Use Case**: Share logic between functional components.
   - **Example**:
     ```javascript
     const useCounter = (initialValue = 0) => {
       const [count, setCount] = useState(initialValue);
       const increment = () => setCount(count + 1);
       return [count, increment];
     };

     const Counter = () => {
       const [count, increment] = useCounter(10);
       return <button onClick={increment}>{count}</button>;
     };
     ```

### Visualization

**1. Presentational and Container Components**:
- **Separation**:
  ```
  Container: Handles data fetching
     ↓
  Presentational: Handles UI rendering
  ```

**2. Higher-Order Components (HOC)**:
- **Enhancement**:
  ```
  Base Component
     ↓
  Enhanced Component (with added logic)
  ```

**3. Render Props**:
- **Sharing Logic**:
  ```
  Parent Component
     ↓
  Render Function: Passed down to handle rendering with shared logic
  ```

**4. Custom Hooks**:
- **Reusability**:
  ```
  Custom Hook
     ↓
  Multiple Components using the shared logic
  ```

### Benefits
- **Modularity**: Easier maintenance and testing.
- **Reusability**: Components and logic can be reused across the application.
- **Readability**: Clear separation of concerns.

These patterns ensure cleaner, more maintainable, and reusable React code.
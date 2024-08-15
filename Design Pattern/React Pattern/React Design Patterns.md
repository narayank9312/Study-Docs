### React Design Patterns

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
     class UserListContainer extends React.Component {
       state = { users: [] };

       componentDidMount() {
         fetch('/api/users')
           .then(response => response.json())
           .then(users => this.setState({ users }));
       }

       render() {
         return <UserList users={this.state.users} />;
       }
     }
     ```

2. **Higher-Order Components (HOC)**:
   - **Use Case**: Reuse component logic.
   - **Example**:
     ```javascript
     const withLoading = Component => {
       return class WithLoading extends React.Component {
         state = { loading: true };

         componentDidMount() {
           this.setState({ loading: false });
         }

         render() {
           return this.state.loading ? <div>Loading...</div> : <Component {...this.props} />;
         }
       };
     };

     const UserListWithLoading = withLoading(UserList);
     ```

3. **Render Props**:
   - **Use Case**: Share logic between components using a prop that is a function.
   - **Example**:
     ```javascript
     class MouseTracker extends React.Component {
       state = { x: 0, y: 0 };

       handleMouseMove = event => {
         this.setState({ x: event.clientX, y: event.clientY });
       };

       render() {
         return (
           <div onMouseMove={this.handleMouseMove}>
             {this.props.render(this.state)}
           </div>
         );
       }
     }

     const App = () => (
       <MouseTracker render={({ x, y }) => (
         <h1>The mouse position is ({x}, {y})</h1>
       )} />
     );
     ```

4. **Controlled and Uncontrolled Components**:
   - **Use Case**: Form handling.
   - **Example**:
     ```javascript
     // Controlled Component
     class ControlledInput extends React.Component {
       state = { value: '' };

       handleChange = event => {
         this.setState({ value: event.target.value });
       };

       render() {
         return <input type="text" value={this.state.value} onChange={this.handleChange} />;
       }
     }

     // Uncontrolled Component
     class UncontrolledInput extends React.Component {
       handleSubmit = event => {
         event.preventDefault();
         console.log(this.input.value);
       };

       render() {
         return (
           <form onSubmit={this.handleSubmit}>
             <input type="text" ref={input => this.input = input} />
             <button type="submit">Submit</button>
           </form>
         );
       }
     }
     ```

5. **Context API**:
   - **Use Case**: Pass data through the component tree without prop drilling.
   - **Example**:
     ```javascript
     const ThemeContext = React.createContext('light');

     const ThemedButton = () => (
       <ThemeContext.Consumer>
         {theme => <button className={theme}>Themed Button</button>}
       </ThemeContext.Consumer>
     );

     const App = () => (
       <ThemeContext.Provider value="dark">
         <ThemedButton />
       </ThemeContext.Provider>
     );
     ```

6. **Custom Hooks**:
   - **Use Case**: Share logic between functional components.
   - **Example**:
     ```javascript
     const useCounter = (initialValue = 0) => {
       const [count, setCount] = React.useState(initialValue);
       const increment = () => setCount(count + 1);
       return [count, increment];
     };

     const Counter = () => {
       const [count, increment] = useCounter(10);
       return <button onClick={increment}>{count}</button>;
     };
     ```

### Explanation and Benefits:

1. **Presentational and Container Components**: Separates UI from business logic, making components easier to manage and test.
2. **Higher-Order Components (HOC)**: Enhances components with additional functionality.
3. **Render Props**: Shares logic using a function prop, offering flexibility.
4. **Controlled and Uncontrolled Components**: Handles form inputs in different ways, offering control and simplicity.
5. **Context API**: Avoids prop drilling by providing a way to pass data through the component tree.
6. **Custom Hooks**: Encapsulates and reuses stateful logic in functional components.

These patterns help in writing clean, reusable, and maintainable React code.
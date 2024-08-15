

These methods are used to control the context (`this` keyword) in JavaScript functions.

#### `call`
**Usage**: Invokes a function with a specified `this` value and arguments provided individually.

**Example**:
```javascript
function greet(greeting, punctuation) {
  console.log(`${greeting}, ${this.name}${punctuation}`);
}

const person = { name: 'Alice' };
greet.call(person, 'Hello', '!'); // "Hello, Alice!"
```

#### `apply`
**Usage**: Similar to `call`, but arguments are provided as an array.

**Example**:
```javascript
greet.apply(person, ['Hi', '...']); // "Hi, Alice..."
```

#### `bind`
**Usage**: Creates a new function that, when called, has `this` set to a specified value.

**Example**:
```javascript
const greetPerson = greet.bind(person, 'Hey', '!');
greetPerson(); // "Hey, Alice!"
```

### Differences
- **`call`**: Immediately invokes the function with individual arguments.
- **`apply`**: Immediately invokes the function with arguments as an array.
- **`bind`**: Returns a new function with bound context and optional initial arguments.

### Practical Use Cases
- **Function borrowing**: Borrow methods from other objects.
- **Partial application**: Create partially applied functions.
- **Event handling**: Ensure the correct context in event handlers.

Understanding these methods enhances your ability to manage context in JavaScript, leading to more predictable and maintainable code.

### Function Borrowing: Borrow Methods from Other Objects

**Example**:
```javascript
const person = {
  name: 'Alice',
  greet() {
    console.log(`Hello, ${this.name}`);
  }
};

const anotherPerson = { name: 'Bob' };
person.greet.call(anotherPerson); // "Hello, Bob"
```

### Partial Application: Create Partially Applied Functions

**Example**:
```javascript
function multiply(a, b) {
  return a * b;
}

const double = multiply.bind(null, 2);
console.log(double(5)); // 10
```

### Event Handling: Ensure Correct Context in Event Handlers

**Example**:
```javascript
class Button {
  constructor(label) {
    this.label = label;
  }

  handleClick() {
    console.log(`Button ${this.label} clicked`);
  }
}

const myButton = new Button('Submit');
document.getElementById('myButton').addEventListener('click', myButton.handleClick.bind(myButton));
```

### Explanation:

1. **Function Borrowing**: Using `call` to borrow `greet` method from `person` and use it on `anotherPerson`.
2. **Partial Application**: Using `bind` to create a `double` function that always multiplies by 2.
3. **Event Handling**: Using `bind` to ensure `handleClick` retains the correct `this` context.
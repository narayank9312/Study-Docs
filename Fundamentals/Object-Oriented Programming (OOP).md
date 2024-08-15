### Object-Oriented Programming (OOP) in JavaScript

#### Key Concepts:

1. **Encapsulation**:
   - **Definition**: Bundling the data and methods that operate on the data into a single unit called an object.
   - **Purpose**: Restricts direct access to some of an object's components, preventing accidental modification of data.
   - **Example**:
     ```javascript
     class Car {
       constructor(make, model) {
         this._make = make;
         this._model = model;
       }

       getMake() {
         return this._make;
       }

       getModel() {
         return this._model;
       }
     }
     ```

2. **Inheritance**:
   - **Definition**: Mechanism by which one class can inherit attributes and methods from another class.
   - **Purpose**: Promotes code reuse and establishes a natural hierarchy.
   - **Example**:
     ```javascript
     class Vehicle {
       constructor(make, model) {
         this.make = make;
         this.model = model;
       }
     }

     class Car extends Vehicle {
       constructor(make, model, numDoors) {
         super(make, model);
         this.numDoors = numDoors;
       }
     }
     ```

3. **Polymorphism**:
   - **Definition**: Ability to present the same interface for different underlying data types.
   - **Purpose**: Allows for methods to be used interchangeably, enhancing flexibility and integration.
   - **Example**:
     ```javascript
     class Animal {
       speak() {
         console.log("Animal sound");
       }
     }

     class Dog extends Animal {
       speak() {
         console.log("Woof!");
       }
     }

     class Cat extends Animal {
       speak() {
         console.log("Meow!");
       }
     }

     const animals = [new Dog(), new Cat()];
     animals.forEach(animal => animal.speak());
     ```

4. **Abstraction**:
   - **Definition**: Hiding the complex implementation details and showing only the essential features of the object.
   - **Purpose**: Simplifies complexity and reduces code duplication.
   - **Example**:
     ```javascript
     class Shape {
       constructor() {
         if (new.target === Shape) {
           throw new TypeError("Cannot construct Shape instances directly");
         }
       }

       area() {
         throw new Error("Method 'area()' must be implemented.");
       }
     }

     class Rectangle extends Shape {
       constructor(width, height) {
         super();
         this.width = width;
         this.height = height;
       }

       area() {
         return this.width * this.height;
       }
     }

     const rectangle = new Rectangle(10, 20);
     console.log(rectangle.area()); // Output: 200
     ```

### Summary:

- **Encapsulation**: Restricts access to certain components.
- **Inheritance**: Allows classes to inherit features from other classes.
- **Polymorphism**: Uses a unified interface for different data types.
- **Abstraction**: Hides complex implementation details.
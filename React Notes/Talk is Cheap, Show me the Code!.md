

---

# Namaste React - Episode 4

## Talk is Cheap, Show me the Code!

🚀 **Namaste-React**

💡 Please make sure to follow along with the whole "Namaste React" series, starting from Episode-1 and continuing through each subsequent episode. The notes are designed to provide detailed explanations of each concept along with examples to ensure thorough understanding. Each episode builds upon the knowledge gained from the previous ones, so starting from the beginning will give you a comprehensive understanding of React development.

💡 I've got a quick tip for you. To get the most out of these notes, it's a good idea to watch Episode-3 first. Understanding what "Akshay" shares in the video will make these notes way easier to understand.

## Recap of Previous Episodes

- Learned what’s JSX.
- Explored what is transpilation and Babel.
- Understood the difference between Class-Based Components and Functional Components.
- Explored the concept of bundlers.
- Learned what is component composition.

## Part 1: Starting a New Project

In this episode, we will start actual coding by starting a new project. Our app is going to be a Food Ordering App.

### Planning for the UI

Before we start coding, plan things out. Planning will make things easier to understand. We should know exactly what to build:

- Name the App
- UI Structure

#### Header

- Logo
- Nav Items

#### Body

- Search
- Restaurant Container
  - Restaurant Card
    - Dish Name
    - Image
    - Restaurant Name
    - Rating
    - Cuisines
    - Time to Deliver

#### Footer

- Copyright
- Links
- Address
- Contact

Keep that as a reference and start coding the app.

### Let’s Start Coding!

It is recommended that you code on your own but for some examples, we have mentioned some pieces for you along with the component name.

**Main components = AppLayout**

```jsx
const AppLayout = () => {
  return (
    <div className="app">
      <Header/>
      <Body/>
    </div>
  );
}
```

**Header Component**

```jsx
const Header = () => {
  return (
    <div className="header">
      <div className="logo-container">
        <img className="logo" src="url" />
      </div>
      <div className="nav-items">
        <ul>
          <li>Home</li>
          <li>About Us</li>
          <li>Contact Us</li>
          <li>Cart</li>
        </ul>
      </div>
    </div>
  );
}
```

### Inline Styling

Writing the CSS along with the element in the same file. It is not recommended to use inline styling. So you should avoid writing it.

```jsx
<div 
  className="red-card" 
  style={{ backgroundColor: "#f0f0f0" }}
>
  <h3> Meghana Foods </h3>
</div>
```

In `style={{ backgroundColor: "#f0f0f0" }}`, the first bracket is to tell that whatever is coming next will be JavaScript and the second bracket is for the JavaScript object.

Or you can store the CSS in a variable and then use it:

```jsx
const styleCard = { backgroundColor: "#f0f0f0" };

<div 
  className="red-card" 
  style={styleCard}
>
  <h3> Meghana Foods </h3>
</div>
```

## Part 2: Introducing Props

Short form for properties. To dynamically send data to a component, we use props. Passing a prop to a function is like passing an argument to a function.

### Passing Props to a Component

Example:

```jsx
<RestaurantCard
  resName="Meghana Foods"
  cuisine="Biryani, North Indian"
/>
```

‘resName’ and ‘cuisine’ are props and this is prop passing to a component.

### Receiving Props in the Component

Props will be wrapped and sent in a JavaScript object.

Example:

```jsx
const RestaurantCard = (props) => {
  return (
    <div>{props.resName}</div>
  );
}
```

### Destructuring Props

Example:

```jsx
const RestaurantCard = ({ resName, cuisine }) => {
  return (
    <div>{resName}</div>
  );
}
```

## Config Driven UI

It is a user Interface that is built and configured using a declaration configuration file or data structure, rather than being hardcoded.

Config is the data coming from the API which keeps on changing according to different factors like user, location, etc.

### Adding Something in the Elements of Array

Example: Adding “,” after every value.

```jsx
resData.data.cuisine.join(", ")
```

### Good Practices

**Destructuring props:**

Optional Chaining

Example:

```jsx
const { name, avgRating, cuisine } = resData?.data;
```

### Dynamic Component Listing using JS map() function

To loop over an array and pass the data to a component once instead of hard coding the same component with different props values.

Avoid ❌

```jsx
<RestaurantCard
  resName="Meghana Foods"
/>
<RestaurantCard
  resName="KFC"
/>
<RestaurantCard
  resName="McDonald's"
/>
<RestaurantCard
  resName="Dominos"
/>
```

Follow ✅

```jsx
const resList = [
  {
    resName: "Meghana Foods"
  },
  {
    resName: "KFC"
  },
  {
    resName: "McDonald's"
  },
  {
    resName: "Dominos"
  }
]

const Body = () => {
  return (
    <div>
      {resList.map((restaurant) => (
        <RestaurantCard resData={restaurant} />
      ))}
    </div>
  );
}
```

### Unique Key id while using map

Each item in the list must be uniquely identified.

**Why?**

When we have components at the same level and if a new component comes first without ID, DOM is going to re-render all the components again. As DOM can’t identify where to place it.

But if we give each of them a unique ID, then React knows where to put that component according to the ID. It is a good optimization and performance thing.

**Note:** Never use index as keys in map. It is not recommended.

```jsx
const Body = () => {
  return (
    <div>
      {resList.map((restaurant) => (
        <RestaurantCard key={restaurant.id} resData={restaurant} />
      ))}
    </div>
  );
}
```

---


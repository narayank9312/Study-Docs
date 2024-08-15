Here is the content of the fifth episode formatted for Obsidian, with code snippets exactly as you specified:

---

# Namaste React - Episode 5

## Let’s Get Hooked!

🚀 **Namaste-React**

💡 Please make sure to follow along with the whole "Namaste React" series, starting from Episode-1 and continuing through each subsequent episode. The notes are designed to provide detailed explanations of each concept along with examples to ensure thorough understanding. Each episode builds upon the knowledge gained from the previous ones, so starting from the beginning will give you a comprehensive understanding of React development.

💡 I've got a quick tip for you. To get the most out of these notes, it's a good idea to watch Episode-5 first. Understanding what "Akshay" shares in the video will make these notes way easier to understand.

## Recap of Previous Episodes

- Built a food ordering app that displayed restaurant cards using real-time data from an API (like Swiggy's).
- Explored the concept of config-driven UI.

## Part 1: Introducing React-Hooks

Before we begin, the first thing we need to do is clean up our app. Up until now, we've placed all our components inside a single `App.js` file, but this isn't considered good practice. It's best to create separate files for each component.

**Q: How can we achieve this?**

To achieve this, let's discuss the folder structure. Currently, all our files are located at the root level of our project.

We are going to restructure our project folder "NAMASTE-REACT." There is a very good convention in the industry that all the code in a React project is kept in a `src` folder. There is no compulsion to use a `src` folder in a project, but here we are following what the industry follows.

We are creating and moving our `App.js` file in the `src` folder, and whatever new files we create, we put them in the `src` folder.

📢 NOTE: Don't forget to update the path of the `App.js` file in `index.html`; otherwise, we will get an error.

The best practice is to make separate files for every component. We have the following components:

1. Header
2. RestaurantCard
3. Body

We put all the above components inside a folder named `components` (child-folder) which has been placed inside the `src` folder (parent folder). When we are creating separate component files inside the `components` folder, always start with a capital letter.

In this course, we are using `.js` as an extension.

1. Header.js
2. RestaurantCard.js
3. Body.js

📢 NOTE: There is no thumb rule to use this convention; we could use any folder structure we wish.

### Understanding Export and Import in React

There are two types of export/import in React. We will understand each of them in detail.

1. Default export/import.
2. Named export/import.

As we know, we move each component's code and create new files individually. Still, our React project throws an error because our `App.js` file doesn't have components in it, and we are using components inside the `App.js`. To solve this, we need to import the components from their respective files which have been kept inside the `components` folder in `src`.

To understand it well, let's take an example of the `Header.js` component.

**Example:**

The `Header.js` component is missing in `App.js`, so we are not able to use it. If we try to use it, it throws an error. To solve this, we have to import `Header.js` inside the `App.js`, and before the import, we have to first export `Header.js` component.

#### 1. Default export/import

**Step-1 (export):**

We use the `export` and `default` keywords with the component name at the end of the component file.

```jsx
// Syntax
export default Header;

// Or we can write with extension.
export default Header.js;
```

**Step-2 (import):**

```jsx
// Syntax
import Header from "./components/Header";
```

📢 NOTE:

1. If you are using VS-Code Editor during import, it automatically tracks the path of the component and gives suggestions to us, so we don't have to worry about the path.
2. We don't have to put an extension in the file in the import statement. If you want to put it, then it's completely fine.

Follow the same method for the rest of the components.

In the case of `RestaurantCard`, we are using it inside the body component.

**Step-1 (export):** Exporting `RestaurantCard.js`

**Step-2 (import):** Importing `RestaurantCard.js` inside the `Body.js`

If we attempt to run our project, we'll encounter the `resLists not defined` error. This happens because `resList` is being used inside `Body.js` without being defined in that file. While one solution is moving `resLists` inside `Body.js`, it's not considered the best practice.

📢 NOTE:

`resList` contains hard-coded data, and we never put any hard-coded data like the source URL of logos and images inside the component file. That's not the best practice the industry follows.

**Q: So where should we keep it?**

We've established a new directory within the `src` folder called `utils`, and inside it, we've created a file named `constants.js` to store all hard-coded data. You can choose any name for this file, but we've opted for lowercase letters since it's not a component. Additionally, we've included the source of logos and images in this file.

We've stored our mock data for `resList` in a file named `mockData.js`, which resides within the `utils` folder.

We need to export data from `constants.js` and `mockData.js`, and then import it into the necessary component files where it will be used.

But there's a catch: If we intend to export multiple items simultaneously from a single file, `default export/import` won't work; it'll result in an error. Instead, we can employ `named export/import` to handle this scenario effectively.

#### 2. Named export/import

Just write the `export` keyword before the variables we want to export.

**Step-1 (export):**

```jsx
// Syntax
export const LOGO_URL = "some-url";
export const CDN_URL = "some-url";
```

**Step-2 (import):**

When we import, there is a slight difference in syntax; we use curly braces.

```jsx
// Syntax
import { LOGO_URL } from "./utils/constants";
import { CDN_URL } from "./utils/constants";
```

📢 NOTE: We can use default export with named export.

## Part 2: Making the App More Lively

In this tutorial series, we're learning by actually building things. As we go along, we'll keep adding new features to our app.

For now, we're going to add a button. When you click on this button, it will show you the best-rated restaurants.

Inside the body component, instead of having a search box, let's replace it with a `<button>`. We'll add this button inside a `<div>` and give it any class name we want. Similarly, we'll also give a class name to the button, as per our preference.

We are adding `onclick` event handler inside the button. `onclick` has a callback function which will be called when we click on the button. There is a condition: when we click on the button, we will get a restaurant which avg-rating is more than 4.2 (`avg-rating > 4.2`).

**Q: How are these cards coming on the screen?**

These cards appear on the screen because we're using the `map()` method to go through each restaurant in our mock data (`resList`). This method helps us display the information from each restaurant on individual cards. So anything changes in `resList`, the cards displayed on the screen will also change.

We're simplifying our mock data to improve our understanding, or you can use the data provided below (which is the actual data from the Swiggy API).

```jsx
let listOfRestaurant = [
  {
    data: {
      id: "255655",
      name: "Cake & Cream",
      cloudinaryImageId: "ac57cc371e73f96f812613f58457aca3",
      areaName: "Jairaj Nagar",
      costForTwo: "₹200 for two",
      cuisines: ["Bakery", "Hot-dog", "pastery", "Cake", "Thick-shake"],
      avgRating: 4.3,
      veg: true,
      parentId: "54670",
      avgRatingString: "4",
      totalRatingsString: "20+",
    },
  },
  {
    data: {
      id: "350363",
      name: "Haldiram's Sweets and Namkeen",
      cloudinaryImageId: "25c3a7d394d6c5556b134385f7d665b0",
      avgRating: 4.6,
      veg: true,
      cuisines: [
        "North Indian",
        "South Indian",
        "Chinese",
        "Pizzas",
        "Fast Food",
      ],
      parentId: "391465",
      avgRatingString: "4.6",
      totalRatingsString: "100+",
    },
  },
  {
    data: {
      id: "154891",
      name: "Rasraj Restaurant",
      cloudinaryImageId: "egbr63ulc8h1zgliivd8",
      locality: "Civil Line",
      areaName: "Civil Lines",
      costForTwo:

 "₹250 for two",
      cuisines: [
        "North Indian",
        "South Indian",
        "Street Food",
        "Chinese",
        "Pizzas",
        "Fast Food",
      ],
      avgRating: 4.2,
    },
  },
  {
    data: {
      id: "745961",
      name: "Balaji Restaurant",
      cloudinaryImageId: "b8672fe52944c3599ea324d99d608300",
      locality: "Sai Rubber Stamp",
      areaName: "Jairaj Nagar",
      costForTwo: "₹149 for two",
      cuisines: ["South Indian", "North Indian"],
      avgRating: 4.8,
      veg: true,
    },
  },
  {
    data: {
      id: "798745",
      name: "Friends Restaurant",
      cloudinaryImageId: "b14cd9fc40129fcfb97aa7e621719d07",
      locality: "Gayatri Nagar",
      areaName: "Jairaj Nagar",
      costForTwo: "₹150 for two",
      cuisines: ["North Indian", "Chinese", "Biryani", "Tandoor", "Kebabs"],
      avgRating: 4.2,
      parentId: "84308",
    },
  },
  {
    data: {
      id: "314737",
      name: "RASOI the KITCHEN",
      cloudinaryImageId: "yjymo9nhyn7rhvafsrd3",
      locality: "Sriram Chowk",
      areaName: "Bazar Ward",
      costForTwo: "₹200 for two",
      cuisines: ["North Indian", "Maharashtrian", "Chinese", "Thalis"],
      avgRating: 3.9,
      parentId: "167341",
    },
  },
  {
    data: {
      id: "201454",
      name: "Morsels restaurants",
      cloudinaryImageId: "aafe71251ef5328784652dc838cd91f3",
      locality: "Bazar Ward",
      areaName: "Chandrapur Locality",
      costForTwo: "₹300 for two",
      cuisines: ["North Indian", "South Indian"],
      avgRating: 3.2,
      veg: true,
      parentId: "139266",
      avgRatingString: "4.2",
    },
  },
  {
    data: {
      id: "266124",
      name: "Trimurti Restaurant",
      cloudinaryImageId: "8135c0066b06e2925c66930be4e9ffb5",
      locality: "Bazar Ward",
      areaName: "Chandrapur Locality",
      costForTwo: "₹150 for two",
      cuisines: ["Desserts"],
      avgRating: 3.9,
      veg: true,
      parentId: "217751",
      avgRatingString: "4.4",
    },
  },
  {
    data: {
      id: "509254",
      name: "Saha Restaurant",
      cloudinaryImageId: "z1ez4uc9idul2uj2v87g",
      areaName: "Jairaj Nagar",
      costForTwo: "₹300 for two",
      cuisines: ["North Indian", "Biryani", "Thalis", "Beverages"],
      avgRating: 3.7,
      parentId: "174585",
      avgRatingString: "3.7",
    },
  },
];
```

We utilize the data mentioned above, incorporating a condition within the callback function. This condition triggers when we click on the button, displaying only the restaurants whose average rating is above 4.2.

Despite implementing the code, no visible changes occur on the screen. However, we successfully filter the data, which we can confirm by checking the filtered results using `console.log(filterlogic)`.

📢 NOTE:

Whenever we have a React App, we have a UI layer and data layer. The UI layer will display what is being sent by the data layer.

**Q: How can we display filtered restaurants dynamically on UI (display screen)?**

Here, we're utilizing data retrieved from the `listOfRestaurant` variable, which stores an array of objects. It's treated as a regular variable within our codebase. However, for this functionality, we require a superpowerful React variable known as a ‘state variable’.

**Q: How do we create a super-powerful variable?**

For that, we use ‘React Hooks’.

**Q: What is a Hook?**

It's simply a regular JavaScript function. However, it becomes powerful when used within React, as it's provided to us by React itself. These pre-built functions have underlying logic developed by React developers. When we install React via npm, we gain access to these superpowers.

Two crucial hooks we frequently utilize are:

1. `useState()`
2. `useEffect()`

**1. useState()**

First, we have to import it as a named import from `react`.

```jsx
import { useState } from "react";

// syntax of useState()
const [listOfRestaurant, setListOfRestaurant] = useState([]);
```

In the provided code, we pass an empty array `[]` as the initial value inside the `useState([])` method. This empty array serves as the default value for the `listOfRestaurant` variable.

If we pass the `listOfRestaurant` where we stored all the restaurant data inside the `useState()` as the default data, it will render the restaurants on the screen using that initial data.

**Q: How could we modify the list of restaurants?**

To modify, we pass the second argument `setListOfRestaurant`. We can name it as we wish. `setListOfRestaurant` is used to update the list.

```jsx
import { useState } from "react";

// syntax of useState()
const [listOfRestaurant, setListOfRestaurant] = useState([]);
```

**Q: How can we display filtered restaurants dynamically on UI (display screen)?** 

We are using `setListOfRestaurant` inside the callback function to show the filtered restaurant. On clicking the button, we will see the updated top-rated restaurant.

```jsx
<button
  className="filter-btn"
  onClick={() => {
    const filtertheRestaurant = listOfRestaurant.filter((res) => {
      return res.data.avgRating > 4.2;
    });
    setListOfRestaurant(filtertheRestaurant);
  }}
>
  Top Rated Restaurant
</button>;
```

📢 NOTE:

- The crucial point about State variables is that whenever they update, React triggers a reconciliation cycle and re-renders the component.
- This means that as soon as the data layer changes, React promptly updates the UI layer. The data layer is always kept in sync with the UI layer.
- To achieve this rapid operation, React employs a reconciliation algorithm, also known as the diffing algorithm or React-Fiber which we will delve into further below.

React is often praised for its speed, have you ever wondered why? 🤔

At the core lies React-Fiber - a powerhouse reimplementation of React's algorithm. The goal of React Fiber is to increase its suitability for areas like animation, layout, and gestures. Its headline feature is incremental rendering: the ability to split rendering work into chunks and spread it out over multiple frames.

These days, we can use JavaScript and React alongside popular libraries like GSAP (GreenSock Animation Platform) and Three.js. These tools allow us to create animations and 3D designs using the capabilities of JavaScript and React.

But how does it all work behind the scenes?

When you create elements in React, you're actually creating virtual DOM objects. These virtual replicas are synced with the real DOM, a process known as "Reconciliation" or the React "diffing" algorithm.

Essentially, every rendering cycle compares the new UI blueprint (updated VDOM) with the old one (previous VDOM) and makes precise changes to the actual DOM accordingly.

It's important to understand these fundamentals in order to unlock a world of possibilities for front-end developers!

Do you want to understand and dive deep into it?

Take a look at this awesome React Fiber architecture repository on the web: [React Fiber Architecture](https://github.com/acdlite/react-fiber-architecture)

---


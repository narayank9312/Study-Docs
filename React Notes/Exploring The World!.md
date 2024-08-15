Sure, here is the complete content of the sixth episode, fully detailed and formatted for Obsidian with code snippets enclosed in triple backticks:

---

# Namaste React - Episode 6

## Exploring The World!

🚀 **Namaste-React**

💡 Please make sure to follow along with the whole "Namaste React" series, starting from Episode-1 and continuing through each subsequent episode. The notes are designed to provide detailed explanations of each concept along with examples to ensure thorough understanding. Each episode builds upon the knowledge gained from the previous ones, so starting from the beginning will give you a comprehensive understanding of React development.

💡 I've got a quick tip for you. To get the most out of these notes, it's a good idea to watch Episode-6 first. Understanding what "Akshay" shares in the video will make these notes way easier to understand.

---

### Two Quick Stories

#### Atlassian's Shift
Back in 2018, Atlassian faced some growing pains. To keep up with demand and stay flexible, they switched to microservices. This move helped them stay agile and scale up smoothly.

#### Netflix's Transformation
The popular video streaming platform Netflix runs on AWS. They started with a monolith and moved to microservices.

---

## PART-1: Monolithic and Microservices Architectures

### What are Monolithic and Microservices Architectures?

**Monolithic Architecture:**
In the past, we used to build large projects where everything was bundled together. Imagine building an entire application where all the code—APIs, user interface, database connections, authentication, even notification services—resides in one massive project with a single code base.

**Issues with Monolithic Architecture:**
- Size and Complexity Limitation
- Slow Startup
- Full Deployment Required
- Limited Change Understanding
- Difficult Continuous Deployment
- Scaling Challenges
- Reliability Concerns
- Adoption of New Technologies

**Microservices Architecture:**
The idea is to split your application into a set of smaller, interconnected services instead of building a single monolithic application. Each service handles a specific job, like handling user accounts or managing payments.

**Advantages of Microservices:**
- Simpler Development
- Independent Teams
- Flexibility in Technology
- Continuous Deployment
- Scalability
- Separation of Concerns
- Single Responsibility

### Why Microservices?

Breaking things down into microservices helps us work faster and smarter. We can update or replace each piece without causing a fuss. It's like having a well-oiled machine where each part does its job perfectly.

### How do these services interact with each other?

In our setup, the UI microservice is written in React, which handles the user interface.

**Communication Channels:**
These services interact with each other through various communication channels. For instance, the UI microservice might need data from the backend microservice, which in turn might need to access the database.

**Ports and Domain Mapping:**
Each microservice runs on its specific port. This means that different services can be deployed independently, with each one assigned to a different port. All these ports are then mapped to a domain name, providing a unified access point for the entire application.

---

## PART-2: Connecting to the External World

In this episode, we're going to explore how our React application communicates with the outside world. We'll dive into how our application fetches data and seamlessly integrates it into the user interface. It's all about understanding data exchange that makes our app come alive.

### Fetching Data

In our Body component, we're displaying a list of restaurants. Initially, we used mock data inside the `useState()` hook to create a state variable. However, in this episode, we're stepping up our game by fetching real-time data from Swiggy's API and displaying it dynamically on the screen. How cool is that? 🤩

### Two Approaches to Fetch and Render Data

1. **Load and Render:**
   - Make the API call as soon as the app loads, fetch the data, and render it.
2. **Render First, Fetch Later:**
   - Quickly render the UI when the page loads (showing the structure of the web page), then make the API call and re-render the application to display the updated information.

In React, we're opting for the second approach. This approach enhances user experience by rendering the UI swiftly and then seamlessly updating it once we receive the data from the API call.

### Use of `useEffect()`

`useEffect()` is a Hook React provides us to help manage our components. It is a regular JavaScript function.

**Importing `useEffect`:**

```jsx
import { useEffect } from "react";

// Syntax of useEffect()
// We passed an arrow function as the callback function.
useEffect(() => {}, []);
```

**When will the callback function get called inside the `useEffect()`?**

The callback function is called after the whole component gets rendered.

### Fetching Data with `fetch()`

We use `fetchData()` function to fetch data from the external world. The logic of fetching the data is exactly the same as in JavaScript.

```jsx
import { useState, useEffect } from "react";

const Body = () => {
  const [listOfRestaurant, setListOfRestaurant] = useState([]);

  useEffect(() => {
    fetchData();
  }, []);

  const fetchData = async () => {
    const data = await fetch(
      "https://www.swiggy.com/dapi/restaurants/list/v5?lat=19.9615398&lng=79.2961468&is-seo-homepage-enabled=true&page_type=DESKTOP_WEB_LISTING"
    );
    const json = await data.json();
    setListOfRestaurant(
      json.data.cards[4].card.card.gridElements.infoWithStyle.restaurants
    );
  };

  return (
    <div>
      {listOfRestaurant.map((restaurant) => (
        <div key={restaurant.info.id}>{restaurant.info.name}</div>
      ))}
    </div>
  );
};

export default Body;
```

### Handling CORS

**CORS (Cross-Origin Resource Sharing)** is a security feature implemented by browsers that restricts web pages from making requests to a different origin than the one from which it was served.

To prevent CORS errors when using APIs, utilize a CORS extension and activate it.

---

## PART-3: Adding a Loading Spinner

After fetching the data, there's a noticeable one-second delay before it appears on the screen. This delay occurs because the APIs take some time to load. Improving this can enhance the user experience.

### Enhancing User Experience with a Shimmer UI

```jsx
if (listOfRestaurant.length === 0) {
  return <h1>Loading...</h1>;
}
```

Instead of displaying a generic "loading" message, we'll integrate a `<Shimmer />` component within our app to provide visual feedback while data is loading.

```jsx
if (listOfRestaurant.length === 0) {
  return <Shimmer />;
}
```

---

## PART-4: Search Functionality

### Creating a Search Bar

```jsx
const [searchText, setSearchText] = useState("");

<div className="search">
  <input
    type="text"
    className="search-box"
    value={searchText}
    onChange={(e) => setSearchText(e.target.value)}
  />
  <button
    className="searchBtn"
    onClick={() => {
      console.log(searchText);
    }}
  >
    Search
  </button>
</div>;
```

### Implementing Case-Insensitive Search

```jsx
<button
  className="searchBtn"
  onClick={() => {
    const filteredRestaurant = listOfRestaurant.filter((res) => {
      return res.info.name.toLowerCase().includes(searchText.toLowerCase());
    });
    setListOfRestaurant(filteredRestaurant);
  }}
>
  Search
</button>;
```

### Managing State Variables

**Why do we need State variables?**

To ensure UI updates reflect changes in state variables, we use `useState()`.

```jsx
const [reactBtn, setReactBtn] = useState("login");

return (
  <div className="container header">
    <a>logo</a>
    {navItems}
    <button
      className="login"
      onClick={() => {
        reactBtn === "login"
          ? setReactBtn("logout")
          : setReactBtn("login");
      }}
    >
      {reactBtn}
    </button>
  </div>
);
```

### Final Code

```jsx
import { useState, useEffect } from "react";
import RestaurantCard from "./RestaurantCard";
import Shimmer from "./Shimmer";

const Body = () => {
  const [listOfRestaurant, setListOfRestaurant] = useState([]);
  const [filteredRestaurant, setFilteredRestaurant] = useState([]);
  const [searchText, setSearchText] = useState("");

  useEffect(() => {
    fetchData();
  }, []);

  const fetchData = async () => {
    const data = await fetch(
      "https://www.swiggy.com/dapi/restaurants/list/v5?lat=19.9615398&lng=79.2961468&is-seo-homepage-enabled=true&page_type=DESKTOP_WEB_LISTING"
    );
    const json = await data.json();
    setListOfRestaurant(
      json?.data?.cards[4]?.card?.card?.gridElements?.infoWithStyle?.restaurants
    );
    setFilteredRestaurant(
      json?.data?.cards[4]?.card?.card?.gridElements?.infoWithStyle?.restaurants
    );
  };

  return listOfRestaurant.length === 0 ? (
    <Shimmer />
  ) : (
    <div className="container body">
      <div className="filter-btn">
        <div class

Name="search">
          <input
            type="text"
            className="search-box"
            value={searchText}
            onChange={(e) => setSearchText(e.target.value)}
          />
          <button
            className="searchBtn"
            onClick={() => {
              const filteredRestaurant = listOfRestaurant.filter((res) => {
                return res.info.name
                  .toLowerCase()
                  .includes(searchText.toLowerCase());
              });
              setFilteredRestaurant(filteredRestaurant);
            }}
          >
            Search
          </button>
        </div>
        <button
          onClick={() => {
            const filterLogic = listOfRestaurant.filter((res) => {
              return res.info.avgRating > 4;
            });
            setFilteredRestaurant(filterLogic);
          }}
        >
          Top Restaurants
        </button>
      </div>
      <div className="ReastaurantContainer">
        {filteredRestaurant.map((restaurant) => (
          <RestaurantCard key={restaurant.info.id} resData={restaurant} />
        ))}
      </div>
    </div>
  );
};

export default Body;
```

---

This Markdown content is structured for easy copying and pasting into Obsidian. It includes important highlights and code snippets formatted with triple backticks for better readability.
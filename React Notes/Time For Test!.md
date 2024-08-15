Here is the complete content of the thirteenth episode formatted for Obsidian, with code snippets exactly as you specified:

---

# Namaste React - Episode 13

## Time For Test!

🚀 **Episode-13 | Time For Test!**

💡 Please make sure to follow along with the whole "Namaste React" series, starting from Episode-1 and continuing through each subsequent episode. The notes are designed to provide detailed explanations of each concept along with examples to ensure thorough understanding. Each episode builds upon the knowledge gained from the previous ones, so starting from the beginning will give you a comprehensive understanding of React development.

💡 I've got a quick tip for you. To get the most out of these notes, it's a good idea to watch Episode-13 first. Understanding the video will make these notes way easier to understand.

---

### In this episode, we are going to learn about:
- What are test cases and how to write them
- Types and importance of testing

👉 Before we start to learn today's episode:
There are many types of testing like QA and developer. But we will learn about developer testing because it's a huge domain in itself.

#### Part-1: Types of testing:
1. **Manual Testing**: Testing the functionality that we have developed. For example, we have developed a search bar, manual testing is checking the search bar manually by searching the query.

💡 This is not a very efficient way because we can’t test every new feature in a big application. A single line can introduce bugs in our whole app because multiple components are connected to each other.

2. **Automatic Testing**: We can write the test cases for testing the functionality. It includes:
   - **Unit Testing**: Write test cases for specific parts (isolated components).
   - **Integration Testing**: Writing test cases for the components that are connected, like the menu page and cart page.
   - **End-to-End Testing**: Writing test cases from the point a user enters the website to when they leave the website.

#### Install Libraries:
📢 NOTE: If you are using `create-react-app` or `vite`, please ignore these installation steps because these packages already include the testing library.

1. **React Testing Library**: It is provided by React and allows testing React components.
```bash
npm i -D @testing-library/react
```

2. **jest**: React Testing Library uses jest, so we need to install it.
```bash
npm i -D jest
```

Since we are using Babel as a bundler, we need to install some extra libraries.
For more details, check the official website: [Jest](https://jestjs.io/) and [Babel](https://babeljs.io/docs/usage).

3. **Install Extra Babel Libraries**:
```bash
npm install --save-dev @babel/core @babel/cli @babel/preset-env
```

4. **Create `babel.config.js`**:
```javascript
const presets = [
  [
    "@babel/preset-env",
    {
      targets: {
        edge: "17",
        firefox: "60",
        chrome: "67",
        safari: "11.1",
      },
      useBuiltIns: "usage",
      corejs: "3.6.4",
    },
  ],
];

module.exports = { presets };
```

📢 NOTE: If you are following this series, then you must know Parcel is using Babel. We just added the `babel.config.js` file, but Parcel also has a Babel configuration behind it that creates a conflict. To solve this, we have to disable the Parcel config. Create a `.parcelrc` file:
```json
{
  "extends": "@parcel/config-default",
  "transformers": {
    "*.{js,mjs,jsx,cjs,ts,tsx}": [
      "@parcel/transformer-js",
      "@parcel/transformer-react-refresh-wrap"
    ]
  }
}
```

To check that you have installed successfully without an error, try to run the test case:
```bash
npm run test  // This will give "no test case found"
```

5. **Configure Jest**:
```bash
npx jest --init  // Executing the jest package
```

After running this command, you have to select some options.

💡 We are using jsdom as a test environment. When we run test cases, there is no browser or server. For running the test cases, we need an environment which is jsdom.

6. **Install jsdom Environment**:
```bash
npm install --save-dev jest-environment-jsdom
```

#### Start Writing Test Cases:
Let's start with writing test cases for a simple function that returns the sum of two numbers.

1. **Create a file for which we need to write the test case**:
```javascript
// sum.js
export const sum = (a, b) => {
  return a + b;
}
```

2. **Create a folder `__test__` and create a file in this folder**:
```javascript
// __test__/sum.test.js
import { sum } from "../components/sum";

test("Function should calculate the sum of two numbers", () => {
  const result = sum(3, 4);  // Call the function
  expect(result).toBe(7);    // Assertion provided by jest
});
```

3. **Run the Test Case**:
I hope now you have an overview of how testing works. So now let's write the original test case for our project.

#### Unit Test:
Let's write a test case to check the component is loading or not. To check any component loads or not, we need to check in the jsdom.
```javascript
test('check component loads or not', () => {
  render(<Contactus />);  // Render the component
  const heading = screen.getByRole("heading");  // Check the specific element
  expect(heading).toBeInTheDocument();  // Check if heading is in the document
});
```

📢 Note: If you are using Parcel, you will encounter an error. The error is we haven’t enabled JSX yet, so we are not able to render the component that uses JSX. Let's enable it.

To enable JSX in the testing environment:
1. **Install Babel**:
```bash
npm i -D @babel/preset-react
```

2. **Set Babel Config**:
📢 Note: Install one more library to use the DOM functions.
```bash
npm i -D @testing-library/jest-dom
```

Now, run the test case. It will pass.

We found the heading using `getByRole`, but we can also find it using different functions like:
```javascript
const button = screen.getByText("submit");  // It will find the text "submit"
expect(button).toBeInTheDocument();
```

💡 We can use it instead of the test keyword to write multiple test cases:
```javascript
describe('To test the header component', () => {
  it("Should load the header component", () => {});
  it("Should include the button", () => {});
});
```

💡 After creating the test case, git will show many files changed. We don’t need to upload the coverage folder to GitHub. So, add coverage to the `.gitignore` file.

Let's make one more test case for testing the Header to check if the button is rendered or not:
```javascript
// Import render and header 
it("should test header component", () => {
  render(<Header />);
});
```

We will get a few errors because we are testing the isolated component.

📢 Note: We used redux store in the header (useSelector), but the store is provided to the app component. To test the Header component, we need to provide the store to the Header component as well.

📢 Note: We used the Link component provided by react-router-dom, but we have provided the router to the App component. So, to test the Header we have to provide the router to the Header component.

To check the button click, you can use the fireEvent which behaves like an onClick method.

#### Integration Testing:

💡 To run the test automatically, make a script in the package.json like `"watch-test": "jest --watch"`. Now we can simply run:
```bash
npm run watch-test
```

Let's write the test case for the Search component. It should show the card in the body when we search for some restaurant.

Fetch the body component first (because the search bar is in the body):
```javascript
it("should show the search button", () => {
  render(<Body />);  // This will throw an error 
});
```

📢 Note: Error generated because the Body component uses the fetch function which is provided by the browser. But we are using jsdom. So, we need to make a mock fetch function with mock data that will replace the original fetch function.

For creating the fetch function, we need to create mock data for the restaurant list. So, create a new file Mock_Data and store the data by copying the restaurant list from the API.

Create our fetch function similar to the browser fetch function:
```javascript
// Import mock Data
global.fetch = jest.fn(() => {
  return Promise.resolve({  // fetch function returns a promise
    json: () => {  // json the promise
      return Promise.resolve(Mock_Data);  // Return mock data
    }
  });
});

// Mock_Data will be returned in the end from the fetch function
it("should show the search button", () => {
  render(<Body />);  // This will throw an error 
});
```

Run this test, we will get the warning.

💡 When we use async operation, we should wrap our component inside the act function. It will return a promise. Also, provide the router to

 the component because we are using the `<Link />`:
```javascript
import { act } from "react-dom/test-utils";
// Import mock Data
global.fetch = jest.fn(() => {
  return Promise.resolve({  // fetch function returns a promise
    json: () => {  // json the promise
      return Promise.resolve(Mock_Data);  // Return mock data
    }
  });
});

// Mock_Data will be returned in the end from the fetch function
it("should show the search button", async () => {
  await act(async () => {
    render(
      <BrowserRouter>  // Because we are using Link
        <Body />
      </BrowserRouter>
    );
  });

  const searchBtn = screen.getByRole("button", { name: "Search" });
  expect(searchBtn).toBeInTheDocument();  // Check the button
});
```

Now, all test cases will pass successfully.

💡 If you don’t want to find using getByRole, we can also use getByTestId. It will always work.

To use getByTestId, give the testid to the element:
```javascript
<input data-testid="searchinput" type="text" />
const searchInput = screen.getByTestId("searchInput");
```

Now, test the input to get the user query to give the restaurant data:
```javascript
const searchInput = screen.getByTestId("searchInput");
// fireEvent is provided by jest which is used to perform the event
fireEvent.change(searchInput, { target: { value: "burger" } });  // Change the input value
fireEvent.click(SearchButton);  // Click the search button

Now, find the restaurant card rendered on the screen after clicking the search button.

💡 To get the restaurant data div, give the testid:
```javascript
const searchCards = screen.getAllByTestId("resCard");  // Get the restaurant cards
expect(searchCards.length).toBe(2);  // Expect the count that shows two cards
```

Now, all test cases will pass.

💡 If we want to write something before and after all the test cases or each test case, jest provides functions:

Final code for Integration testing:
```javascript
import { fireEvent, render, screen } from "@testing-library/react";
import Body from "../components/Body";
import { BrowserRouter } from "react-router-dom";
import MockResList from "../__tests__/mocks/MockResList.json";
import { act } from "react-dom/test-utils";

global.fetch = jest.fn(() => {
  return Promise.resolve({
    json: () => {
      return Promise.resolve(MockResList);
    }
  });
});

// describe is used to club multiple test cases
describe("", () => {
  // to print before all test cases
  beforeAll(() => {
    console.log("Before test case");
  });

  // to print before each test case
  beforeEach(() => {
    console.log("Before Each");
  });

  // to print after all test cases
  afterAll(() => {
    console.log("After test cases");
  });

  // to print after each test case
  afterEach(() => {
    console.log("After each");
  });

  it("Should render body component with search feature", async () => {
    await act(async () => 
      render(
        <BrowserRouter>
          <Body />
        </BrowserRouter>
      )
    );
  });

  it("Should search ResList for burger text input", async () => {
    await act(async () => 
      render(
        <BrowserRouter>
          <Body />
        </BrowserRouter>
      )
    );

    const TotalCards = screen.getAllByTestId("resCard");
    expect(TotalCards.length).toBe(18);

    const SearchButton = screen.getByRole("button", { name: "Search" });
    
    const searchInput = screen.getByTestId("searchInput");
    fireEvent.change(searchInput, { target: { value: "burger" } });
    fireEvent.click(SearchButton);

    const searchCards = screen.getAllByTestId("resCard");
    expect(searchCards.length).toBe(2);
  });

  it("Should filter Top rated restaurant after clicking button", async () => {
    await act(async () => 
      render(
        <BrowserRouter>
          <Body />
        </BrowserRouter>
      )
    );

    const TotalCards = screen.getAllByTestId("resCard");
    expect(TotalCards.length).toBe(18);

    const Button = screen.getByRole("button", { name: "Top Rated" });
    fireEvent.click(Button);

    const searchCards = screen.getAllByTestId("resCard");
    expect(searchCards.length).toBe(6);
  });

  it("should render Username", async () => {
    await act(async () => 
      render(
        <BrowserRouter>
          <Body />
        </BrowserRouter>
      )
    );

    const userInput = screen.getByTestId("userInput");
    expect(userInput.value).toBe("Gourav");
  });
});
```

---

This Markdown content is structured for easy copying and pasting into Obsidian. It includes important highlights and code snippets formatted with triple backticks for better readability.
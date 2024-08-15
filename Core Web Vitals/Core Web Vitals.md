### Core Web Vitals

Core Web Vitals are a set of metrics defined by Google to measure the user experience of a website. These metrics focus on three key aspects: loading performance, interactivity, and visual stability.

1. **Largest Contentful Paint (LCP)**:
   - **Definition**: Measures loading performance. LCP marks the point in the page load timeline when the main content has likely loaded.
   - **Good LCP**: Less than 2.5 seconds.
   - **Example**:
     ```html
     <img src="large-image.jpg" alt="Large Image" width="600" height="400">
     ```

2. **First Input Delay (FID)**:
   - **Definition**: Measures interactivity. FID quantifies the delay between the user's first interaction with a page and the browser's response to that interaction.
   - **Good FID**: Less than 100 milliseconds.
   - **Example**:
     ```html
     <button onclick="handleClick()">Click Me</button>
     <script>
       function handleClick() {
         // Some interaction logic
       }
     </script>
     ```

3. **Cumulative Layout Shift (CLS)**:
   - **Definition**: Measures visual stability. CLS scores the sum total of all individual layout shift scores for every unexpected layout shift that occurs during the entire lifespan of the page.
   - **Good CLS**: Less than 0.1.
   - **Example**:
     ```html
     <style>
       img { display: block; width: 100%; height: auto; }
     </style>
     <img src="image.jpg" alt="Image" />
     ```

### Example in React:

```javascript
import React, { useEffect } from 'react';

const App = () => {
  useEffect(() => {
    // Example of measuring LCP, FID, and CLS
    const reportWebVitals = (metric) => {
      console.log(metric);
    };

    import('web-vitals').then(({ getLCP, getFID, getCLS }) => {
      getLCP(reportWebVitals);
      getFID(reportWebVitals);
      getCLS(reportWebVitals);
    });
  }, []);

  return (
    <div>
      <h1>Core Web Vitals Example</h1>
      <img src="large-image.jpg" alt="Large Image" width="600" height="400" />
      <button onClick={() => console.log('Button clicked!')}>Click Me</button>
    </div>
  );
};

export default App;
```

### Summary:

- **LCP**: Measures loading performance. Aim for < 2.5s.
- **FID**: Measures interactivity. Aim for < 100ms.
- **CLS**: Measures visual stability. Aim for < 0.1.

These metrics help ensure a good user experience by focusing on performance and stability.
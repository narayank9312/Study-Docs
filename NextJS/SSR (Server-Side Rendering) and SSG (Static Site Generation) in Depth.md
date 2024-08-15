### SSR (Server-Side Rendering) and SSG (Static Site Generation) in Depth

Both SSR and SSG are methods of pre-rendering content in web applications, which helps improve performance, SEO, and user experience. Let's dive into each method with practical examples and detailed flow diagrams.

### Server-Side Rendering (SSR)

**Server-Side Rendering (SSR)** is a technique where the HTML content of a webpage is generated on the server for each request. This means every time a user requests a page, the server processes the request, renders the HTML, and sends it to the client.

#### Key Concepts:
- **Dynamic Content**: HTML is generated dynamically for each request.
- **SEO Friendly**: Search engines can crawl the fully rendered HTML.
- **Faster First Load**: Users see the fully rendered page faster compared to client-side rendering.

#### Practical Example with Next.js:

1. **Setting Up Next.js Project**:
   ```bash
   npx create-next-app ssr-example
   cd ssr-example
   ```

2. **Creating SSR Page**:
   **pages/index.js**:
   ```javascript
   import React from 'react';

   export async function getServerSideProps() {
       // Fetch data from an API or database
       const res = await fetch('https://api.example.com/data');
       const data = await res.json();

       return { props: { data } };
   }

   const Home = ({ data }) => {
       return (
           <div>
               <h1>Server-Side Rendering Example</h1>
               <pre>{JSON.stringify(data, null, 2)}</pre>
           </div>
       );
   };

   export default Home;
   ```

3. **Running the Server**:
   ```bash
   npm run dev
   ```

4. **Viewing the Application**:
   - Open `http://localhost:3000` to see the server-rendered HTML with data fetched from the API.

#### Flow Diagram:

1. **User Request**:
   - User requests a page.
2. **Server Processing**:
   - Server fetches data.
   - Server generates HTML.
3. **Response**:
   - Server sends HTML to the client.
4. **Client**:
   - Client renders the HTML.

```plaintext
+--------+                +---------+                 +--------+
| Client |  ------------> |  Server | ------------->  | Client |
|        |   Request      |         |    Response     |        |
+--------+                +---------+                 +--------+
                              |
                              v
                     +-------------------+
                     | Fetch Data & Render|
                     +-------------------+
```

### Static Site Generation (SSG)

**Static Site Generation (SSG)** is a technique where the HTML content of a webpage is generated at build time. This means the HTML is pre-rendered into static files and served to the client, resulting in faster load times and improved performance.

#### Key Concepts:
- **Static Content**: HTML is generated once at build time.
- **SEO Friendly**: Search engines can crawl the pre-rendered HTML.
- **Faster Subsequent Loads**: Static files are served quickly by the CDN.

#### Practical Example with Next.js:

1. **Setting Up Next.js Project**:
   ```bash
   npx create-next-app ssg-example
   cd ssg-example
   ```

2. **Creating SSG Page**:
   **pages/index.js**:
   ```javascript
   import React from 'react';

   export async function getStaticProps() {
       // Fetch data from an API or database
       const res = await fetch('https://api.example.com/data');
       const data = await res.json();

       return { props: { data } };
   }

   const Home = ({ data }) => {
       return (
           <div>
               <h1>Static Site Generation Example</h1>
               <pre>{JSON.stringify(data, null, 2)}</pre>
           </div>
       );
   };

   export default Home;
   ```

3. **Building the Project**:
   ```bash
   npm run build
   npm run start
   ```

4. **Viewing the Application**:
   - Open `http://localhost:3000` to see the pre-rendered HTML with data fetched from the API.

#### Flow Diagram:

1. **Build Time**:
   - Data is fetched and HTML is generated.
   - HTML is stored as static files.
2. **User Request**:
   - User requests a page.
3. **Response**:
   - Static HTML is served to the client.

```plaintext
+--------+                +--------+                 +--------+
| Client |  ------------> | Server | ------------->  | Client |
|        |   Request      |        |    Response     |        |
+--------+                +--------+                 +--------+
                         (Static Files)
```

### Differences Between SSR and SSG

- **SSR**:
  - Generates HTML on each request.
  - Suitable for dynamic content that changes frequently.
  - Higher server load due to rendering on each request.

- **SSG**:
  - Generates HTML at build time.
  - Suitable for static content that does not change frequently.
  - Faster load times due to serving static files.

### Conclusion

Both SSR and SSG have their use cases in modern web development. SSR is ideal for dynamic content that changes frequently, providing up-to-date content on each request. SSG is perfect for static content, offering faster load times and reduced server load by serving pre-rendered static files.

### References

- [Next.js Documentation](https://nextjs.org/docs)
- [MDN Web Docs - Server-Side Rendering (SSR)](https://developer.mozilla.org/en-US/docs/Web/Performance/Server-side_rendering)
- [MDN Web Docs - Static Site Generators](https://developer.mozilla.org/en-US/docs/Learn/Tools_and_testing/Client-side_JavaScript_frameworks/Static_site_generation)
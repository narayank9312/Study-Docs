
---

# Namaste React - Episode 2

## Igniting Our App!

🚀 **Namaste-React**

💡 Please make sure to follow along with the whole "Namaste React" series, starting from Episode-1 and continuing through each subsequent episode. The notes are designed to provide detailed explanations of each concept along with examples to ensure thorough understanding. Each episode builds upon the knowledge gained from the previous ones, so starting from the beginning will give you a comprehensive understanding of React development.

💡 I've got a quick tip for you. To get the most out of these notes, it's a good idea to watch Episode-2 first. Understanding what "Akshay" shares in the video will make these notes way easier to understand.

## Recap of Episode-1

- Learned about Libraries, Frameworks, and their differences.
- Created "Hello World!" using HTML, JavaScript, and React.
- Studied Emmet and CORS (Cross-Origin Resource Sharing).

## Igniting Our App

**Q: To make our app production-ready, what should we do?**

- Minify our file (Remove console logs, bundle things up).
- Need a server to run things.

📢 **NOTE:** Minify → Optimization → Clean console → Bundle.

### Bundlers

A bundler is a tool that bundles our app, packages our app so that it can be shipped to production.

**Examples of Bundlers:**
- Webpack
- Vite
- Parcel

📢 **NOTE:** In create-react-app, the bundler used is Webpack.

### Package Manager

Bundlers are packages. If we want to use a package in our code, we have to use a package manager.

**We use a package manager known as npm or yarn.**

### Configuring the Project

```bash
npm init
```

This creates a `package.json` file.

To install parcel:

```bash
npm install -D parcel
```

This will generate a `package-lock.json` file.

### package.json

`package.json` file is a configuration for NPM. Whatever packages our project needs, we install those packages using:

```bash
npm install <packageName>
```

Once package installation is complete, their versions and configuration-related information are stored as dependencies inside the `package.json` file.

### package-lock.json

`package-lock.json` locks the exact version of packages being used in the project.

**Difference between package.json and package-lock.json:**

In `package.json`, we have information about the generic version of installed packages, whereas in `package-lock.json`, we have information about the specific or exact version of installed packages.

### node_modules

This gets installed as a database for npm. Every dependency in `node_module` will have its `package.json`.

📢 **NOTE:** Never touch `node_modules` and `package-lock.json`.

### Igniting Our App

To ignite our app:

```bash
npx parcel index.html
```

- `npx` means ‘execute using npm’.
- `index.html` is the entry point.

### Hot Module Replacement (HMR)

It means that Parcel will keep track of all the files which you are updating.

- There is a File Watcher Algorithm (written in C++). It keeps track of all the files which are changing in real-time and it tells the server to reload.

### parcel-cache

Parcel caches code all the time. When we run the application, a build is created which takes some time in ms. If we make any code changes and save the application, another build will be triggered which might take even less time than the previous build. This reduction of time is due to the parcel cache.

Parcel immediately loads the code from the cache every time there is a subsequent build. On the very first build, Parcel creates a folder `.parcel-cache` where it stores the caches in binary code format.

Parcel gives faster build, faster developer experience because of caching.

### dist

It keeps the files minified for us. When the bundler builds the app, the build goes into a folder called `dist`.

The `/dist` folder contains the minimized and optimized version of the source code. Along with the minified code, the `/dist` folder also comprises all the compiled modules that may or may not be used with other systems.

### Production Build

To create a faster development version of our project and serve it on the server:

```bash
npx parcel index.html
```

To make a production build:

```bash
npx parcel build index.html
```

Parcel will build all the production files to the `dist` folder.

### Parcel Features at a Glance

- Hot Module Replacement (HMR)
- File Watcher Algorithm - C++
- Bundling
- Minify Code
- Cleaning our code
- Dev and production build
- Super fast build algorithm
- Image Optimization
- Caching while development
- Compression
- Compatible with older browser versions
- HTTPS on dev
- Image Optimization
- Port No
- Consistency Hashing Algorithm
- Zero Config
- Tree Shaking

### Transitive Dependencies

We have our package manager which takes care of our transitive dependencies of our code.

### Browserslist

Browserslist is a tool that specifies which browsers should be supported/compatible in your frontend app. It makes our code compatible with a lot of browsers.

In `package.json` file do:

```json
"browserslist": [
  "> 1%",
  "last 2 versions"
]
```

### Tree Shaking

Tree shaking is a process of removing the unwanted code that we do not use while developing the application. In computing, tree shaking is a dead code elimination technique that is applied when optimizing code.

---


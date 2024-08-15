To convert the provided notes into an Obsidian format with flow diagrams and coding examples, I will structure the content with appropriate Markdown formatting and embed code snippets and placeholders for flow diagrams.

### Episode 1: Introduction to React

#### Inception!

🚀 **Namaste-React**

💡 Please make sure to follow along with the whole "Namaste React" series, starting from Episode-1 and continuing through each subsequent episode. The notes are designed to provide detailed explanations of each concept along with examples to ensure thorough understanding. Each episode builds upon the knowledge gained from the previous ones, so starting from the beginning will give you a comprehensive understanding of React development.

💡 I've got a quick tip for you. To get the most out of these notes, it's a good idea to watch Episode-1 first. Understanding what "Akshay" shares in the video will make these notes way easier to understand.

#### Introduction to React

**Q1: What is React? Why is React known as ‘React’?**

React is a JavaScript Library. The name ‘React’ was chosen because the library was designed to allow developers to react to changes in state and data within an application, and to update the user interface in a declarative and efficient manner.

**Q2: What is a Library?**

A library is a collection of prewritten code snippets that can be used and reused to perform certain tasks. A particular JavaScript library code can be plugged into application code which leads to faster development and fewer vulnerabilities to errors.

**Examples**: React, jQuery

**Q3: What is a Framework?**

A framework provides a basic foundation or structure for a website or an application.

**Examples**: Angular

**Q4: Similarities between Library and Framework?**

Frameworks and libraries are code written by third parties to solve regular/common problems or to optimize performance.

**Q5: Difference between Library and Framework?**

A key difference between the two is Inversion of Control. When using a library, the control remains with the developer who tells the application when to call library functions. When using a framework, the control is reversed, which means that the framework tells the developer where code needs to be provided and calls it as it requires.

#### Emmet

Emmet is the essential toolkit for web developers. It allows you to type shortcuts that are then expanded into full-fledged boilerplate code for writing HTML and CSS.

#### Coding Examples

**Q6: Create Hello World Program using only HTML**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Hello World</title>
</head>
<body>
    <h1>Hello World</h1>
</body>
</html>
```

**Q7: Create Hello World Program using only JavaScript**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Hello World</title>
    <script>
        document.addEventListener("DOMContentLoaded", function() {
            document.body.innerHTML = "<h1>Hello World</h1>";
        });
    </script>
</head>
<body>
</body>
</html>
```

**Q8: Create Hello World Program using only React**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Hello World</title>
</head>
<body>
    <div id="root"></div>
    <script src="https://unpkg.com/react@17/umd/react.development.js" crossorigin></script>
    <script src="https://unpkg.com/react-dom@17/umd/react-dom.development.js" crossorigin></script>
    <script>
        const e = React.createElement;
        ReactDOM.render(
            e('h1', null, 'Hello World'),
            document.getElementById('root')
        );
    </script>
</body>
</html>
```

#### Cross-Origin Resource Sharing (CORS)

The `crossorigin` attribute in the script tag enables Cross-Origin Resource Sharing (CORS) for loading external JavaScript files from a different origin than the hosting web page. This allows the script to access resources from the server hosting the script, such as making HTTP requests or accessing data.

**Q9: What does {} denote in React code?**

This (`id='title'`), classes, etc. should come under `{}`. Whenever something is passed inside `{}`, it will go as tag attributes of `h1`.

📢 **NOTE**: React will overwrite everything inside "root" and replace it with whatever is given inside `render`.

### Flow Diagram

> ![Flow Diagram](flow-diagram-placeholder.png)
> 
> Placeholder for a flow diagram to visualize the relationship between libraries and frameworks, and the concept of inversion of control.

### Building Structure in React

To build the following structure in React:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Hello World</title>
</head>
<body>
    <div id="root"></div>
    <script src="https://unpkg.com/react@17/umd/react.development.js" crossorigin></script>
    <script src="https://unpkg.com/react-dom@17/umd/react-dom.development.js" crossorigin></script>
    <script>
        const e = React.createElement;
        ReactDOM.render(
            e('h1', null, 'Hello World'),
            document.getElementById('root')
        );
    </script>
</body>
</html>
```

### Next Steps

Continue to Episode-2 for deeper insights into React development.

---


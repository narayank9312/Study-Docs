Sure, let's go through each of these questions with a detailed explanation and relevant JavaScript code examples.

### 1. What is Event Bubbling?

**Event Bubbling** is a mechanism in the DOM (Document Object Model) where an event starts from the target element and then bubbles up to its parent elements and ancestors. For example, if you have a nested structure and click on the innermost element, the event will propagate from the innermost element to the outermost element.

```html
<div id="outer">
  <div id="inner">Click me</div>
</div>

<script>
  document.getElementById('outer').addEventListener('click', () => {
    console.log('Outer Div Clicked');
  });

  document.getElementById('inner').addEventListener('click', () => {
    console.log('Inner Div Clicked');
  });
</script>
```

If you click on `#inner`, you will see both "Inner Div Clicked" and "Outer Div Clicked" in the console because the event bubbles up from `#inner` to `#outer`.

### 2. Difference between `.on('click')` and `.click()`

- **`.on('click')`**: This is a jQuery method used to attach an event handler function to an element for the click event. It can delegate events, which means it can attach an event handler to current and future elements that match the selector.

```javascript
$(document).on('click', '.button', function() {
  console.log('Button clicked');
});
```

- **`.click()`**: This jQuery method is a shorthand for `.on('click')` but can also be used to trigger the click event.

```javascript
$('.button').click(function() {
  console.log('Button clicked');
});
```

### 3. How can you improve the performance of a site (Only frontend)?

- **Minimize HTTP Requests**: Combine files, use CSS sprites, and reduce the number of elements on a page.
- **Use a Content Delivery Network (CDN)**: Serve your static assets from a CDN to reduce latency.
- **Optimize Images**: Compress images and use appropriate formats.
- **Minify CSS, JavaScript, and HTML**: Remove unnecessary characters.
- **Use Asynchronous Loading for JavaScript**: Use `async` and `defer` for script tags.
- **Lazy Load Images**: Load images only when they are in the viewport.
- **Reduce CSS and JavaScript Complexity**: Simplify and optimize code.
- **Cache Assets**: Use browser caching for static resources.
- **Use HTTP/2**: Enables multiplexing, reducing the number of HTTP requests.

### 4. Write a function to check if two strings are anagram or not

An anagram is a word or phrase formed by rearranging the letters of a different word or phrase.

```javascript
function areAnagrams(str1, str2) {
  const normalize = str => str.replace(/[^a-zA-Z0-9]/g, '').toLowerCase().split('').sort().join('');
  return normalize(str1) === normalize(str2);
}

console.log(areAnagrams('listen', 'silent')); // true
console.log(areAnagrams('hello', 'world')); // false
```

### 5. Difference between `.on('click', function()` and `.click(function())`

- **`.on('click', function())`**: Allows event delegation, which means the event handler can be attached to current and future elements that match the selector.

```javascript
$(document).on('click', '.button', function() {
  console.log('Button clicked');
});
```

- **`.click(function())`**: Directly binds the event handler to the elements that match the selector at the time of binding.

```javascript
$('.button').click(function() {
  console.log('Button clicked');
});
```

### 6. Implement queue with the help of two stacks

A queue follows FIFO (First In First Out) principle, while a stack follows LIFO (Last In First Out).

```javascript
class Queue {
  constructor() {
    this.stack1 = [];
    this.stack2 = [];
  }

  enqueue(element) {
    this.stack1.push(element);
  }

  dequeue() {
    if (this.stack2.length === 0) {
      while (this.stack1.length > 0) {
        this.stack2.push(this.stack1.pop());
      }
    }
    return this.stack2.pop();
  }
}

const q = new Queue();
q.enqueue(1);
q.enqueue(2);
console.log(q.dequeue()); // 1
q.enqueue(3);
console.log(q.dequeue()); // 2
console.log(q.dequeue()); // 3
```

### 7. Find if a number is a power of 2 or not?

```javascript
function isPowerOfTwo(n) {
  return (n > 0) && (n & (n - 1)) === 0;
}

console.log(isPowerOfTwo(4)); // true
console.log(isPowerOfTwo(5)); // false
```

### 8. In how many ways you can display HTML elements?

You can display HTML elements in various ways by setting the CSS `display` property. Some common values are:

- `block`: Displays an element as a block-level element.
- `inline`: Displays an element as an inline element.
- `inline-block`: Displays an element as an inline-level block container.
- `flex`: Displays an element as a block-level flex container.
- `grid`: Displays an element as a block-level grid container.
- `none`: Hides the element.

Example:

```html
<div style="display: block;">Block Element</div>
<span style="display: inline;">Inline Element</span>
<div style="display: inline-block;">Inline-Block Element</div>
<div style="display: flex;">Flex Element</div>
<div style="display: grid;">Grid Element</div>
<div style="display: none;">Hidden Element</div>
```

By understanding these concepts and being able to explain and implement them in JavaScript, you'll be well-prepared for related questions in an interview setting.
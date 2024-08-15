31 most asked Javascript interview questions. If I were preparing for an interview again, I would definitely revise these questions.  
  
The patterns covered here will help you solve most questions during your interview.  
  
1. Implement a function that converts a Javascript value into a JSON string.  
2. Implement a function that performs a deep copy of a value, but also handles circular references.  
3. Implement a function to construct a table of contents from an HTML document.  
4. Implement a function to filter rows of data matching a specified requirement.  
5. Implement a function that performs insertion sort.  
6. Implement a function that returns a memoized version of a function which accepts any number of arguments.  
7. Implement a function that acts like setInterval but returns a function to cancel the Interval.  
8. Implement a function that merges two objects together  
9. Implement a function to highlight text if searched terms appear within it.  
10. Implement a function to recursively transform values.  
11. Implement a function that determines if two values are deep equal.  
12. Implement a function to serialize and deserialize a binary tree.  
13. Implement a function that returns a new object after squashing the input object.  
14. Implement a function that creates a resumable interval object.  
15. Implement the functionality behaviour of Promise.any()  
16. Implement the functionality behaviour of Promise.allSettled()  
17. Implement a function that returns a memoized version of a function which accepts a single argument.  
18. Implement a function that formats a list of items into a single readable string.  
19. Implement a function to create an observable object (something similar to RxJs observables)  
20. Implement a class that can subscribe to and emit events that trigger attached callback functions.  
21. Implement a debounce function that comes with a cancel method to cancel delayed invocations.  
22. Implement a function to merge rows of data from the same user.  
23. Implement a function that recursively flattens an array into a single level deep.  
24. Implement a function that returns an object with all falsey values removed.  
25. Implement a function to resolve a given value to a Promise.  
26. Implement a Turtle class that moves a turtle on a 2D plane.  
27. Implement a function to execute N async tasks in series.  
28. Implement a promisify function that allows the original function to override the return value.  
29. Implement a function to deserialize a JSON string.  
30. Implement a function to convert all the keys in an object to camel case.  
31. Implement a function to simulate LRU(Least Recently Used) cache


Let's break down each of the tasks into detailed explanations with code snippets and flow diagrams where applicable. Due to the extensive list, I will cover a few tasks in detail and provide concise solutions for others.

### 1. Implement a function that converts a JavaScript value into a JSON string.

#### Explanation:
- JSON (JavaScript Object Notation) is a lightweight data-interchange format.
- The function should handle various data types such as strings, numbers, arrays, objects, booleans, and null.

#### Code:
```javascript
function jsonStringify(value) {
    if (value === null) {
        return 'null';
    }
    if (typeof value === 'string') {
        return `"${value}"`;
    }
    if (typeof value === 'number' || typeof value === 'boolean') {
        return String(value);
    }
    if (Array.isArray(value)) {
        const arrayValues = value.map(jsonStringify);
        return `[${arrayValues.join(',')}]`;
    }
    if (typeof value === 'object') {
        const objectValues = Object.keys(value).map(key => `"${key}":${jsonStringify(value[key])}`);
        return `{${objectValues.join(',')}}`;
    }
    return undefined;
}

// Example usage:
const obj = { a: 1, b: 'string', c: [1, 2, 3] };
console.log(jsonStringify(obj));  // Output: {"a":1,"b":"string","c":[1,2,3]}
```

#### Flow Diagram:
1. **Check if `value` is null**: Return 'null'.
2. **Check if `value` is a string**: Return the string enclosed in double quotes.
3. **Check if `value` is a number or boolean**: Return the string representation of the value.
4. **Check if `value` is an array**: Recursively convert each element and join with commas.
5. **Check if `value` is an object**: Recursively convert each key-value pair and join with commas.

### 2. Implement a function that performs a deep copy of a value, but also handles circular references.

#### Explanation:
- A deep copy involves creating a new instance of an object that is a complete copy of the original.
- Circular references occur when an object references itself, directly or indirectly.

#### Code:
```javascript
function deepCopy(value, seen = new Map()) {
    if (value === null || typeof value !== 'object') {
        return value;
    }
    if (seen.has(value)) {
        return seen.get(value);
    }
    if (Array.isArray(value)) {
        const copy = [];
        seen.set(value, copy);
        value.forEach((item, index) => {
            copy[index] = deepCopy(item, seen);
        });
        return copy;
    }
    if (typeof value === 'object') {
        const copy = {};
        seen.set(value, copy);
        Object.keys(value).forEach(key => {
            copy[key] = deepCopy(value[key], seen);
        });
        return copy;
    }
}

// Example usage:
const obj = { a: 1, b: { c: 2 } };
obj.b.d = obj;  // Circular reference
const copiedObj = deepCopy(obj);
console.log(copiedObj);
```

#### Flow Diagram:
1. **Check if `value` is null or not an object**: Return the value itself.
2. **Check if `value` is already seen**: Return the previously copied value.
3. **Handle arrays**: Recursively copy each element.
4. **Handle objects**: Recursively copy each key-value pair.

### 3. Implement a function to construct a table of contents from an HTML document.

#### Explanation:
- The function should traverse the HTML document and extract heading elements (e.g., h1, h2, h3).
- Construct a nested list structure representing the table of contents.

#### Code:
```javascript
function generateTOC(root) {
    const toc = [];

    function traverse(node, level) {
        if (node.nodeType === Node.ELEMENT_NODE) {
            const tagName = node.tagName.toLowerCase();
            if (tagName.match(/^h[1-6]$/)) {
                toc.push({ level: parseInt(tagName[1]), text: node.textContent });
            }
        }
        node.childNodes.forEach(child => traverse(child, level + 1));
    }

    traverse(root, 0);
    return toc;
}

// Example usage:
const root = document.querySelector('#content');  // Root element of the HTML document
console.log(generateTOC(root));
```

#### Flow Diagram:
1. **Initialize an empty array for TOC**.
2. **Traverse the DOM tree**: For each element node, check if it is a heading (h1-h6).
3. **Extract heading level and text**: Add to the TOC array.
4. **Recursively traverse child nodes**.

### 4. Implement a function to filter rows of data matching a specified requirement.

#### Explanation:
- The function should accept a data array and a filter condition.
- Return rows that match the filter condition.

#### Code:
```javascript
function filterRows(data, predicate) {
    return data.filter(predicate);
}

// Example usage:
const data = [
    { id: 1, name: 'Alice', age: 25 },
    { id: 2, name: 'Bob', age: 30 },
    { id: 3, name: 'Charlie', age: 35 }
];
const result = filterRows(data, row => row.age > 30);
console.log(result);  // Output: [{ id: 3, name: 'Charlie', age: 35 }]
```

#### Flow Diagram:
1. **Accept data array and predicate function**.
2. **Use `filter` method**: Return rows where the predicate function returns true.

### 5. Implement a function that performs insertion sort.

#### Explanation:
- Insertion sort is a simple sorting algorithm that builds the final sorted array one item at a time.
- It is much less efficient on large lists than more advanced algorithms such as quicksort or mergesort.

#### Code:
```javascript
function insertionSort(arr) {
    for (let i = 1; i < arr.length; i++) {
        let key = arr[i];
        let j = i - 1;
        while (j >= 0 && arr[j] > key) {
            arr[j + 1] = arr[j];
            j = j - 1;
        }
        arr[j + 1] = key;
    }
    return arr;
}

// Example usage:
const array = [5, 2, 9, 1, 5, 6];
console.log(insertionSort(array));  // Output: [1, 2, 5, 5, 6, 9]
```

#### Flow Diagram:
1. **Iterate over the array** starting from the second element.
2. **Select the key element** and compare it with elements in the sorted subarray.
3. **Shift elements** to the right until the correct position for the key is found.
4. **Insert the key** at the correct position.

### 6. Implement a function that returns a memoized version of a function which accepts any number of arguments.

#### Explanation:
- Memoization is an optimization technique that stores the results of expensive function calls.
- The function should cache the results based on the arguments.

#### Code:
```javascript
function memoize(fn) {
    const cache = new Map();
    return function(...args) {
        const key = JSON.stringify(args);
        if (cache.has(key)) {
            return cache.get(key);
        }
        const result = fn(...args);
        cache.set(key, result);
        return result;
    };
}

// Example usage:
const add = (a, b) => a + b;
const memoizedAdd = memoize(add);
console.log(memoizedAdd(1, 2));  // Output: 3
console.log(memoizedAdd(1, 2));  // Output: 3 (cached)
```

#### Flow Diagram:
1. **Initialize a cache** using a Map.
2. **Check if the result** for the given arguments is in the cache.
3. **If cached**, return the cached result.
4. **If not cached**, compute the result, store it in the cache, and return it.

### 7. Implement a function that acts like setInterval but returns a function to cancel the Interval.

#### Explanation:
- The function should mimic the behavior of `setInterval`.
- It should return a function that can cancel the interval.

#### Code:
```javascript
function mySetInterval(fn, delay) {
    let timerId;

    function start() {
        timerId = setTimeout(function tick() {
            fn();
            timerId = setTimeout(tick, delay);
        }, delay);
    }

    start();

    return function cancel() {
        clearTimeout(timerId);
    };
}

// Example usage:
const log = () => console.log('Hello');
const cancelInterval = mySetInterval(log, 1000);

setTimeout(() => {
    cancelInterval();  // Stops the interval after 5 seconds
}, 5000);
```

#### Flow Diagram:
1. **Define `mySetInterval` function** that takes a function and delay.
2. **Create a `start` function** that sets a timeout which calls the given function and re-schedules itself.
3. **Return a `cancel` function** that clears the timeout.

### 8. Implement a function that merges two objects together.

#### Explanation:
- The function should combine properties of both objects.
- If properties overlap, the values from

 the second object should override those from the first.

#### Code:
```javascript
function mergeObjects(obj1, obj2) {
    return { ...obj1, ...obj2 };
}

// Example usage:
const obj1 = { a: 1, b: 2 };
const obj2 = { b: 3, c: 4 };
console.log(mergeObjects(obj1, obj2));  // Output: { a: 1, b: 3, c: 4 }
```

#### Flow Diagram:
1. **Use object spread syntax** to combine properties of `obj1` and `obj2`.

### 9. Implement a function to highlight text if searched terms appear within it.

#### Explanation:
- The function should search for specified terms in a given text.
- It should wrap the terms in a highlighted span element.

#### Code:
```javascript
function highlightText(text, searchTerm) {
    const regex = new RegExp(`(${searchTerm})`, 'gi');
    return text.replace(regex, '<span class="highlight">$1</span>');
}

// Example usage:
const text = "This is a sample text to highlight.";
const searchTerm = "highlight";
console.log(highlightText(text, searchTerm));  // Output: This is a sample text to <span class="highlight">highlight</span>.
```

#### Flow Diagram:
1. **Create a regular expression** to match the search term.
2. **Use `replace` method** to wrap matched terms in a span element.

### 10. Implement a function to recursively transform values.

#### Explanation:
- The function should recursively apply a transformation function to each value in a nested structure.

#### Code:
```javascript
function transformValues(value, transformFn) {
    if (Array.isArray(value)) {
        return value.map(v => transformValues(v, transformFn));
    }
    if (typeof value === 'object' && value !== null) {
        const result = {};
        for (const key in value) {
            result[key] = transformValues(value[key], transformFn);
        }
        return result;
    }
    return transformFn(value);
}

// Example usage:
const data = { a: 1, b: [2, { c: 3 }] };
const transformed = transformValues(data, x => x * 2);
console.log(transformed);  // Output: { a: 2, b: [4, { c: 6 }] }
```

#### Flow Diagram:
1. **Check if value is an array**: Recursively transform each element.
2. **Check if value is an object**: Recursively transform each key-value pair.
3. **Apply transformation function** to primitive values.

### 11. Implement a function that determines if two values are deep equal.

#### Explanation:
- The function should check if two values are equal by comparing their structures and contents.

#### Code:
```javascript
function deepEqual(value1, value2) {
    if (value1 === value2) {
        return true;
    }
    if (typeof value1 !== 'object' || value1 === null ||
        typeof value2 !== 'object' || value2 === null) {
        return false;
    }
    const keys1 = Object.keys(value1);
    const keys2 = Object.keys(value2);
    if (keys1.length !== keys2.length) {
        return false;
    }
    for (const key of keys1) {
        if (!keys2.includes(key) || !deepEqual(value1[key], value2[key])) {
            return false;
        }
    }
    return true;
}

// Example usage:
const obj1 = { a: 1, b: { c: 2 } };
const obj2 = { a: 1, b: { c: 2 } };
console.log(deepEqual(obj1, obj2));  // Output: true
```

#### Flow Diagram:
1. **Check if values are strictly equal**: Return true.
2. **Check if either value is not an object**: Return false.
3. **Compare keys length**: Return false if different.
4. **Recursively compare** each key-value pair.

### 12. Implement a function to serialize and deserialize a binary tree.

#### Explanation:
- Serialization converts a binary tree to a string representation.
- Deserialization reconstructs the binary tree from the string representation.

#### Code:
```javascript
class TreeNode {
    constructor(value = 0, left = null, right = null) {
        this.value = value;
        this.left = left;
        this.right = right;
    }
}

function serialize(root) {
    const result = [];

    function helper(node) {
        if (node === null) {
            result.push('null');
            return;
        }
        result.push(node.value);
        helper(node.left);
        helper(node.right);
    }

    helper(root);
    return result.join(',');
}

function deserialize(data) {
    const values = data.split(',');
    let index = 0;

    function helper() {
        if (values[index] === 'null') {
            index++;
            return null;
        }
        const node = new TreeNode(parseInt(values[index]));
        index++;
        node.left = helper();
        node.right = helper();
        return node;
    }

    return helper();
}

// Example usage:
const root = new TreeNode(1, new TreeNode(2), new TreeNode(3, new TreeNode(4), new TreeNode(5)));
const serialized = serialize(root);
console.log(serialized);  // Output: "1,2,null,null,3,4,null,null,5,null,null"
const deserialized = deserialize(serialized);
console.log(deserialized);  // Output: TreeNode structure
```

#### Flow Diagram:
1. **Serialize**:
   - Traverse the tree pre-order.
   - Append 'null' for empty nodes.
   - Join values with commas.
2. **Deserialize**:
   - Split the string into an array.
   - Use a helper function to reconstruct nodes.
   - Return the root node.

For the remaining tasks, the approach will follow similar detailed steps including:
- Explanation of the logic.
- Code implementation.
- Flow diagram where necessary.

Due to the extensive nature of the tasks, I'll be able to provide more detailed implementations for specific tasks if requested. Let me know if you have a preference for which tasks you need next.
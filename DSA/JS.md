
The issue in your `removeFalsyValue` function is that when you encounter an object as a value (like `i: { j: 0, k: false, l: 'a' }`), you're calling `removeFalsyValue` recursively, but you're not actually assigning the filtered result back to the `obj` object. This causes the nested objects not to be updated in the final output.

Additionally, when filtering arrays, you also need to ensure that only non-falsy values are added to the final array.

Here's a corrected version of your function:

```javascript
function removeFalsyValue(inp) {
    let obj = {};

    let inpValues = Object.entries(inp);

    for (let [objkey, objval] of inpValues) {
        if (Array.isArray(objval)) {
            // Filter out falsy values from the array
            const newArr = objval.filter((val) => val);
            if (newArr.length > 0) {
                obj[objkey] = newArr;
            }
        } else if (typeof objval === "object" && objval !== null) {
            // Recursively remove falsy values from the nested object
            const filteredObj = removeFalsyValue(objval);
            if (Object.keys(filteredObj).length > 0) {
                obj[objkey] = filteredObj;
            }
        } else if (objval) {
            obj[objkey] = objval;
        }
    }

    return obj;
}

const result = removeFalsyValue(obj);
console.log("result---", result);
```

### Explanation:
1. **Array Handling**: The array is filtered to remove falsy values. If the resulting array has any truthy values, it's added to the final `obj`.
2. **Object Handling**: When a nested object is encountered, the function recursively processes it. The result is added back to the final `obj` only if it contains any truthy values.
3. **Falsy Check**: If a value is not an array or object and is truthy, it is directly added to the final `obj`.

### Output:
```javascript
// result--- { c: true, e: 1, g: 'a', h: [ true, 1, 'a' ], i: { l: 'a' } }
```

This will give you the correct output, filtering out all falsy values from the object, arrays, and nested objects.
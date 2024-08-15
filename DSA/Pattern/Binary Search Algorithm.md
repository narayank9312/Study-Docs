### Binary Search Algorithm

Binary Search is an efficient algorithm for finding an item from a sorted list of items. It works by repeatedly dividing the search interval in half. If the value of the search key is less than the item in the middle of the interval, narrow the interval to the lower half. Otherwise, narrow it to the upper half. Repeatedly check until the value is found or the interval is empty.

### Key Concepts:

1. **Divide and Conquer**:
   - Split the array into halves to reduce the search space.

2. **Sorted Array**:
   - The array must be sorted for binary search to work.

### Implementation in JavaScript:

```javascript
function binarySearch(arr, target) {
  let left = 0;
  let right = arr.length - 1;

  while (left <= right) {
    const mid = Math.floor((left + right) / 2);

    if (arr[mid] === target) {
      return mid;
    } else if (arr[mid] < target) {
      left = mid + 1;
    } else {
      right = mid - 1;
    }
  }

  return -1; // Target not found
}

// Example usage:
const arr = [1, 2, 3, 4, 5, 6, 7, 8, 9];
const target = 4;
console.log(binarySearch(arr, target)); // Output: 3
```

### Detailed Flowchart:

1. **Initialize Pointers**:
   - Start with two pointers, `left` at the beginning and `right` at the end of the array.

2. **Calculate Midpoint**:
   - Calculate `mid` as the average of `left` and `right`.

3. **Compare and Narrow Down**:
   - Compare the `target` with `arr[mid]`.
   - If `target` is equal to `arr[mid]`, return `mid`.
   - If `target` is less than `arr[mid]`, move the `right` pointer to `mid - 1`.
   - If `target` is greater than `arr[mid]`, move the `left` pointer to `mid + 1`.

4. **Repeat Until Found or Empty**:
   - Repeat the process until `left` is greater than `right`.

```plaintext
Initial:
arr = [1, 2, 3, 4, 5, 6, 7, 8, 9]
target = 4
left = 0
right = 8

Iteration 1:
mid = (0 + 8) / 2 = 4
arr[mid] = 5
target < arr[mid]
right = mid - 1 = 3

Iteration 2:
mid = (0 + 3) / 2 = 1
arr[mid] = 2
target > arr[mid]
left = mid + 1 = 2

Iteration 3:
mid = (2 + 3) / 2 = 2
arr[mid] = 3
target > arr[mid]
left = mid + 1 = 3

Iteration 4:
mid = (3 + 3) / 2 = 3
arr[mid] = 4
target == arr[mid]
Return 3
```

### Summary:

- **Binary Search** is efficient for finding an element in a sorted array with O(log n) time complexity.
- It uses a divide-and-conquer approach to narrow down the search space.
- Requires the array to be sorted for proper execution.

### Binary Search Algorithm Recurive way you will find below 

Binary search is an efficient algorithm for finding an item from a sorted list of items. It works by repeatedly dividing in half the portion of the list that could contain the item until you've narrowed down the possible locations to just one.

### Key Concepts:

1. **Sorted Array**:
   - Binary search works on a sorted array.
   - If the array is not sorted, the algorithm will not function correctly.

2. **Divide and Conquer**:
   - The algorithm repeatedly divides the search interval in half.
   - If the value of the search key is less than the item in the middle of the interval, narrow the interval to the lower half.
   - Otherwise, narrow it to the upper half.
   - Repeat until the value is found or the interval is empty.

### Implementation in JavaScript:

#### Iterative Approach:
```javascript
function binarySearch(arr, target) {
  let left = 0;
  let right = arr.length - 1;

  while (left <= right) {
    const mid = Math.floor((left + right) / 2);

    if (arr[mid] === target) {
      return mid;
    } else if (arr[mid] < target) {
      left = mid + 1;
    } else {
      right = mid - 1;
    }
  }

  return -1; // Target not found
}

// Example usage:
const arr = [1, 2, 3, 4, 5, 6, 7, 8, 9];
const target = 5;
console.log(binarySearch(arr, target)); // Output: 4
```

#### Recursive Approach:
```javascript
function binarySearchRecursive(arr, target, left = 0, right = arr.length - 1) {
  if (left > right) {
    return -1; // Target not found
  }

  const mid = Math.floor((left + right) / 2);

  if (arr[mid] === target) {
    return mid;
  } else if (arr[mid] < target) {
    return binarySearchRecursive(arr, target, mid + 1, right);
  } else {
    return binarySearchRecursive(arr, target, left, mid - 1);
  }
}

// Example usage:
console.log(binarySearchRecursive(arr, target)); // Output: 4
```

### Flowchart:

**1. Binary Search Flow**:
```plaintext
Start
|
v
Check if array is sorted
|
v
Initialize left = 0, right = arr.length - 1
|
v
While left <= right:
|
v
Calculate mid = Math.floor((left + right) / 2)
|
v
If arr[mid] == target:
    Return mid
Else If arr[mid] < target
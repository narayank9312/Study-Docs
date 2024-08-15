### Sorting Algorithms: Deep Dive

#### Bubble Sort

**Concept**: Repeatedly steps through the list, compares adjacent elements, and swaps them if they are in the wrong order. This pass-through process is repeated until the list is sorted.

**Complexity**:
- **Best Case**: \(O(n)\)
- **Average Case**: \(O(n^2)\)
- **Worst Case**: \(O(n^2)\)

**Advantages**: Simple to implement.
**Disadvantages**: Inefficient for large datasets.

#### Merge Sort

**Concept**: Divides the list into two halves, recursively sorts each half, and then merges the sorted halves.

**Complexity**:
- **Best Case**: \(O(n \log n)\)
- **Average Case**: \(O(n \log n)\)
- **Worst Case**: \(O(n \log n)\)

**Advantages**: Consistent \(O(n \log n)\) performance, stable sort.
**Disadvantages**: Requires additional memory for the temporary arrays.

**Implementation**:

```javascript
function mergeSort(arr) {
  if (arr.length <= 1) return arr;
  const mid = Math.floor(arr.length / 2);
  const left = mergeSort(arr.slice(0, mid));
  const right = mergeSort(arr.slice(mid));
  return merge(left, right);
}

function merge(left, right) {
  let result = [], i = 0, j = 0;
  while (i < left.length && j < right.length) {
    if (left[i] < right[j]) result.push(left[i++]);
    else result.push(right[j++]);
  }
  return result.concat(left.slice(i)).concat(right.slice(j));
}
```

#### Quick Sort

**Concept**: Selects a 'pivot' element, partitions the array into elements less than and greater than the pivot, and recursively sorts the sub-arrays.

**Complexity**:
- **Best Case**: \(O(n \log n)\)
- **Average Case**: \(O(n \log n)\)
- **Worst Case**: \(O(n^2)\)

**Advantages**: Efficient for large datasets, in-place sort.
**Disadvantages**: Worst-case \(O(n^2)\) time complexity.

**Implementation**:

```javascript
function quickSort(arr) {
  if (arr.length <= 1) return arr;
  const pivot = arr[arr.length - 1];
  const left = [], right = [];
  for (let i = 0; i < arr.length - 1; i++) {
    if (arr[i] < pivot) left.push(arr[i]);
    else right.push(arr[i]);
  }
  return [...quickSort(left), pivot, ...quickSort(right)];
}
```

### Comparison

**Bubble Sort**:
- **Complexity**: \(O(n^2)\)
- **Use Case**: Small or mostly sorted datasets.
- **Characteristics**: Simple but inefficient.

**Merge Sort**:
- **Complexity**: \(O(n \log n)\)
- **Use Case**: Large datasets or when stability is needed.
- **Characteristics**: Consistent performance, extra space required.

**Quick Sort**:
- **Complexity**: Average \(O(n \log n)\), Worst \(O(n^2)\)
- **Use Case**: Large datasets, in-place sorting.
- **Characteristics**: Fastest in practice for most inputs, but can degrade to \(O(n^2)\).

### Summary

- **Bubble Sort**: Simple but inefficient with \(O(n^2)\) complexity.
- **Merge Sort**: Stable and consistently \(O(n \log n)\), requires extra space.
- **Quick Sort**: Generally the fastest \(O(n \log n)\) but can degrade to \(O(n^2)\). 

Understanding the strengths and weaknesses of each algorithm helps in selecting the appropriate sort for a given problem.


Let's explain the `mergeSort` function and how it sorts the given array in ascending order using the Merge Sort algorithm. We'll break down each part of the code and discuss its role in the sorting process.

### Code Explanation

#### mergeSort Function

```javascript
function mergeSort(arr) {
  // Base case: if the array has 0 or 1 element, it is already sorted
  if (arr.length <= 1) return arr;
  
  // Find the middle index
  let mid = Math.floor(arr.length / 2);

  // Recursively sort the left half
  let left = mergeSort(arr.slice(0, mid));

  // Recursively sort the right half
  let right = mergeSort(arr.slice(mid));

  // Merge the sorted halves
  return merge(left, right);
}
```

**Key Points:**

1. **Base Case**: If the array has 0 or 1 element, it is already sorted, so return it.
2. **Dividing the Array**: 
   - Calculate the middle index using `Math.floor(arr.length / 2)`.
   - Split the array into two halves: `left` (from start to mid) and `right` (from mid to end) using the `slice` method.
3. **Recursive Calls**: Recursively apply `mergeSort` to both halves until they reach the base case.
4. **Merging**: Use the `merge` function to combine the sorted halves into a single sorted array.

#### merge Function

```javascript
function merge(left, right) {
  let sortedArr = [];

  // While both arrays have elements
  while (left.length && right.length) {
    if (left[0] < right[0]) {
      // If the first element of left is smaller, push it to the sorted array
      sortedArr.push(left.shift());
    } else {
      // If the first element of right is smaller, push it to the sorted array
      sortedArr.push(right.shift());
    }
  }

  // Concatenate any remaining elements from left or right (one of these will be empty)
  return [...sortedArr, ...left, ...right];
}
```

**Key Points:**

1. **Initialization**: Initialize an empty array `sortedArr` to store the sorted elements.
2. **Merging Process**:
   - Compare the first elements of `left` and `right` arrays.
   - Push the smaller element to `sortedArr` and remove it from its original array using `shift()`.
   - Repeat until one of the arrays is empty.
3. **Concatenation**: Once one of the arrays is empty, concatenate the remaining elements of the non-empty array to `sortedArr`.

### Time Complexity

- **Divide Step**: Each division step takes O(log n) time because the array is repeatedly divided in half.
- **Merge Step**: Merging two halves takes O(n) time because each element is compared and added to the sorted array once.

Overall Time Complexity: O(n log n)

### Space Complexity

- **Auxiliary Space**: The algorithm uses additional space to store the left and right halves and the merged result. The space complexity is O(n) due to the storage requirements for the subarrays.

### Example Walkthrough

Let's go through an example with the input array `[8, 3, 5, 4, 7, 6, 1, 2]`:

1. **Initial Array**: `[8, 3, 5, 4, 7, 6, 1, 2]`
2. **Divide Step**:
   - Split into `[8, 3, 5, 4]` and `[7, 6, 1, 2]`
3. **Recursive Calls**:
   - Split `[8, 3, 5, 4]` into `[8, 3]` and `[5, 4]`
   - Split `[8, 3]` into `[8]` and `[3]` (base case)
   - Split `[5, 4]` into `[5]` and `[4]` (base case)
   - Split `[7, 6, 1, 2]` into `[7, 6]` and `[1, 2]`
   - Split `[7, 6]` into `[7]` and `[6]` (base case)
   - Split `[1, 2]` into `[1]` and `[2]` (base case)

4. **Merge Step**:
   - Merge `[8]` and `[3]` to get `[3, 8]`
   - Merge `[5]` and `[4]` to get `[4, 5]`
   - Merge `[3, 8]` and `[4, 5]` to get `[3, 4, 5, 8]`
   - Merge `[7]` and `[6]` to get `[6, 7]`
   - Merge `[1]` and `[2]` to get `[1, 2]`
   - Merge `[6, 7]` and `[1, 2]` to get `[1, 2, 6, 7]`
   - Merge `[3, 4, 5, 8]` and `[1, 2, 6, 7]` to get `[1, 2, 3, 4, 5, 6, 7, 8]`

### Final Output

The final sorted array is `[1, 2, 3, 4, 5, 6, 7, 8]`.

### Conclusion

Merge Sort is an efficient and stable sorting algorithm that uses a divide-and-conquer strategy to sort arrays. It recursively splits the array into smaller subarrays, sorts them, and then merges them back together in a sorted manner. The algorithm has a time complexity of O(n log n) and a space complexity of O(n).


### Implementing Quick Sort in JavaScript

Quick Sort is an efficient, in-place sorting algorithm that follows the divide-and-conquer paradigm. It works by selecting a 'pivot' element from the array and partitioning the other elements into two sub-arrays, according to whether they are less than or greater than the pivot. The sub-arrays are then sorted recursively.

### Quick Sort Implementation (Using Additional Arrays)

This version of Quick Sort uses additional arrays (`left` and `right`) to hold elements less than and greater than the pivot.

```javascript
function quickSort(arr) {
  if (arr.length <= 1) {
    return arr;
  }

  const pivot = arr[0];
  const left = [];
  const right = [];

  for (let i = 1; i < arr.length; i++) {
    if (arr[i] < pivot) {
      left.push(arr[i]);
    } else {
      right.push(arr[i]);
    }
  }

  return [...quickSort(left), pivot, ...quickSort(right)];
}

// Time Complexity -
// Average Case - O(n log n)
// Best Case - O(n log n)
// Worst Case - O(n^2)

// Space Complexity -
// Average Case - O(log n)
// Worst Case - O(n)

console.log(quickSort([8, 3, 5, 4, 7, 6, 1, 2])); // Output: [1, 2, 3, 4, 5, 6, 7, 8]
```

### Quick Sort Implementation (In-Place)

This version of Quick Sort does not use additional arrays and performs the sorting in place. It modifies the original array and uses a helper function (`pivot`) to partition the array.

```javascript
function quickSort(arr, start = 0, end = arr.length - 1) {
  if (start < end) {
    const pivotIndex = pivot(arr, start, end);
    quickSort(arr, start, pivotIndex - 1);
    quickSort(arr, pivotIndex + 1, end);
  }

  return arr;
}

function pivot(arr, start = 0, end = arr.length - 1) {
  function swap(array, i, j) {
    let temp = array[i];
    array[i] = array[j];
    array[j] = temp;
  }

  let pivot = arr[start];
  let swapIdx = start;

  for (let i = start + 1; i <= end; i++) {
    if (arr[i] < pivot) {
      swapIdx++;
      swap(arr, swapIdx, i);
    }
  }

  swap(arr, start, swapIdx);
  return swapIdx;
}

// Time Complexity -
// Average Case - O(n log n)
// Best Case - O(n log n)
// Worst Case - O(n^2)

// Space Complexity -
// Average Case - O(log n)
// Worst Case - O(n)

console.log(quickSort([8, 3, 5, 4, 7, 6, 1, 2])); // Output: [1, 2, 3, 4, 5, 6, 7, 8]
```

### Detailed Explanation

#### Quick Sort (Using Additional Arrays)

1. **Base Case**: If the array has 0 or 1 element, it is already sorted, so return it.
2. **Choosing a Pivot**: Select the first element as the pivot.
3. **Partitioning**: Iterate through the array, comparing each element with the pivot. Elements less than the pivot are pushed to the `left` array, and elements greater than or equal to the pivot are pushed to the `right` array.
4. **Recursive Sorting**: Recursively apply Quick Sort to the `left` and `right` arrays.
5. **Combining**: Combine the sorted `left` array, the pivot, and the sorted `right` array.

#### Quick Sort (In-Place)

1. **Base Case**: If `start` is not less than `end`, the array is already sorted, so return it.
2. **Pivot Function**: This function partitions the array around a pivot element (chosen as the first element in this example). 
   - **Swapping Elements**: Swap elements to ensure that elements less than the pivot are on its left, and elements greater than or equal to the pivot are on its right.
   - **Returning Pivot Index**: Return the index of the pivot element after partitioning.
3. **Recursive Sorting**: Recursively apply Quick Sort to the sub-arrays before and after the pivot index.

### Time and Space Complexity

**Time Complexity**:
- **Average and Best Case**: O(n log n) - The array is divided roughly in half each time.
- **Worst Case**: O(n²) - This occurs when the pivot selection is poor (e.g., the smallest or largest element), leading to unbalanced partitions.

**Space Complexity**:
- **In-Place Version**: O(log n) for the recursion stack in the average case.
- **With Additional Arrays**: O(n) due to the space required for the additional arrays used for partitioning.

By understanding and implementing these two versions of Quick Sort, you can choose the one that best fits your requirements and constraints in different scenarios.
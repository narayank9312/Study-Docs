### Sliding Window Pattern: Deep Dive

The sliding window pattern is a technique used to solve problems involving a contiguous subarray or substring. It's efficient for problems requiring a running total or maximum within a window that slides through the data structure.

### Key Concepts:

1. **Fixed-Size Window**:
   - Used when the window size is known.
   - Slide the window over the data structure to find the desired result.

2. **Dynamic-Size Window**:
   - Used when the window size can vary.
   - Adjust the window size dynamically based on conditions.

### How to Understand the Pattern:

1. **Identify the Problem Type**:
   - Look for problems involving subarrays or substrings.
   - Check if you need a running sum, maximum, minimum, or count within a window.

2. **Determine Window Size**:
   - For fixed-size windows, determine the size before starting.
   - For dynamic windows, define conditions to expand or shrink the window.

3. **Slide the Window**:
   - Initialize the window at the start of the data structure.
   - Slide the window, updating the result as you move.

### Practice in JavaScript:

#### Example 1: Fixed-Size Window
Find the maximum sum of a subarray of size `k`.

```javascript
function maxSumSubarray(arr, k) {
  let maxSum = 0, windowSum = 0;

  // Calculate the sum of the first window
  for (let i = 0; i < k; i++) {
    windowSum += arr[i];
  }
  maxSum = windowSum;

  // Slide the window
  for (let i = k; i < arr.length; i++) {
    windowSum += arr[i] - arr[i - k];
    maxSum = Math.max(maxSum, windowSum);
  }

  return maxSum;
}

// Example usage
const arr = [1, 2, 3, 4, 5, 6, 7, 8, 9];
const k = 3;
console.log(maxSumSubarray(arr, k)); // Output: 24
```

#### Example 2: Dynamic-Size Window
Find the smallest subarray with a sum greater than or equal to `s`.

```javascript
function minSubarrayLength(arr, s) {
  let minLength = Infinity;
  let windowSum = 0;
  let start = 0;

  for (let end = 0; end < arr.length; end++) {
    windowSum += arr[end];

    while (windowSum >= s) {
      minLength = Math.min(minLength, end - start + 1);
      windowSum -= arr[start];
      start++;
    }
  }

  return minLength === Infinity ? 0 : minLength;
}

// Example usage
const arr = [2, 1, 5, 2, 3, 2];
const s = 7;
console.log(minSubarrayLength(arr, s)); // Output: 2
```

### Flow Diagram:

#### Fixed-Size Window
1. Initialize `windowSum` with the sum of the first `k` elements.
2. Slide the window by adding the next element and removing the first element of the previous window.
3. Update `maxSum` with the maximum value of `windowSum`.

#### Dynamic-Size Window
1. Initialize `windowSum` and `start`.
2. Expand the window by adding elements to `windowSum`.
3. Shrink the window from the left until `windowSum` is less than `s`.
4. Update `minLength` with the minimum size of the current window.

By understanding the sliding window pattern and practicing with these examples, you'll be able to solve a variety of problems involving subarrays and substrings efficiently.
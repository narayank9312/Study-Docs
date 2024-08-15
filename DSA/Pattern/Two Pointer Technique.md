### Two Pointer Technique: Deep Dive

The two-pointer technique is a common strategy used to solve problems that involve searching or processing data within a single array or list. It's particularly effective for problems involving sorted arrays or those requiring pairs or triplets of elements.

### Key Concepts:

1. **Two Pointer Approach**:
   - Involves using two pointers to iterate through the data structure.
   - Pointers can start at the same or opposite ends, depending on the problem.

2. **Common Use Cases**:
   - Finding pairs with a specific sum.
   - Reversing a string or list.
   - Sorting-related problems.

### How to Understand the Pattern:

1. **Identify the Problem Type**:
   - Look for problems involving pairs, triplets, or subarrays.
   - Determine if the array is sorted or needs sorting.

2. **Set Initial Pointers**:
   - Decide the initial positions of the pointers (e.g., start and end, or both at the beginning).

3. **Move Pointers Based on Conditions**:
   - Adjust pointers based on the problem conditions (e.g., move inward for pairs, outward for searching).

### Practice in JavaScript:

#### Example 1: Two Sum Problem (Sorted Array)
Find two numbers in a sorted array that add up to a given target.

```javascript
function twoSumSorted(arr, target) {
  let left = 0, right = arr.length - 1;

  while (left < right) {
    const sum = arr[left] + arr[right];
    if (sum === target) {
      return [arr[left], arr[right]];
    } else if (sum < target) {
      left++;
    } else {
      right--;
    }
  }

  return [];
}

// Example usage
const arr = [1, 2, 3, 4, 6];
const target = 6;
console.log(twoSumSorted(arr, target)); // Output: [2, 4]
```

#### Example 2: Removing Duplicates from Sorted Array
Remove duplicates in place and return the new length.

```javascript
function removeDuplicates(nums) {
  if (nums.length === 0) return 0;

  let left = 0;
  for (let right = 1; right < nums.length; right++) {
    if (nums[left] !== nums[right]) {
      left++;
      nums[left] = nums[right];
    }
  }

  return left + 1;
}

// Example usage
const nums = [1, 1, 2, 2, 3, 3, 4, 4, 5];
console.log(removeDuplicates(nums)); // Output: 5
console.log(nums); // Modified array: [1, 2, 3, 4, 5, ...]
```

### Flow Diagrams:

#### Two Sum Problem
1. **Initialize Pointers**:
   - Left pointer at the start.
   - Right pointer at the end.

2. **Iterate and Adjust Pointers**:
   - If the sum is equal to the target, return the pair.
   - If the sum is less, move the left pointer to the right.
   - If the sum is more, move the right pointer to the left.

```plaintext
Initial Pointers: left = 0, right = arr.length - 1

While left < right:
    sum = arr[left] + arr[right]
    if sum == target:
        return [arr[left], arr[right]]
    else if sum < target:
        left++
    else:
        right--
```

#### Remove Duplicates
1. **Initialize Pointers**:
   - Left pointer to track the position of the last unique element.
   - Right pointer to iterate through the array.

2. **Iterate and Update**:
   - If elements at left and right pointers differ, increment left and update the element at left position.

```plaintext
Initial Pointers: left = 0

For right = 1 to nums.length - 1:
    if nums[left] != nums[right]:
        left++
        nums[left] = nums[right]

Return left + 1
```

By practicing these examples and understanding the flow diagrams, you'll be able to effectively apply the two-pointer technique to solve various problems.
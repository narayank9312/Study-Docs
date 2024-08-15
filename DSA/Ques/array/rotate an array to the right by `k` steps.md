Sure! Let's explore two approaches to rotate an array to the right by `k` steps:

### Using JavaScript Built-in Functions

**Approach**:
1. Calculate the effective rotation using `k % nums.length`.
2. Use `slice` to split the array and `concat` to merge them back.

**Example Code**:
```javascript
function rotateWithBuiltIn(nums, k) {
    k = k % nums.length;
    return nums.slice(-k).concat(nums.slice(0, -k));
}

const nums = [1, 2, 3, 4, 5, 6, 7];
const k = 3;
console.log(rotateWithBuiltIn(nums, k)); // Output: [5, 6, 7, 1, 2, 3, 4]
```

### Without Using JavaScript Built-in Functions

**Approach**:
1. Reverse the entire array.
2. Reverse the first `k` elements.
3. Reverse the rest of the array.

**Example Code**:
```javascript
function reverse(arr, start, end) {
    while (start < end) {
        [arr[start], arr[end]] = [arr[end], arr[start]];
        start++;
        end--;
    }
}

function rotateWithoutBuiltIn(nums, k) {
    k = k % nums.length;
    reverse(nums, 0, nums.length - 1);
    reverse(nums, 0, k - 1);
    reverse(nums, k, nums.length - 1);
}

const nums2 = [1, 2, 3, 4, 5, 6, 7];
const k2 = 3;
rotateWithoutBuiltIn(nums2, k2);
console.log(nums2); // Output: [5, 6, 7, 1, 2, 3, 4]
```

### Explanation of the Non-Built-in Approach

1. **Reverse the Entire Array**:
   - `[1, 2, 3, 4, 5, 6, 7]` becomes `[7, 6, 5, 4, 3, 2, 1]`.

2. **Reverse the First `k` Elements**:
   - `[7, 6, 5, 4, 3, 2, 1]` with `k = 3` becomes `[5, 6, 7, 4, 3, 2, 1]`.

3. **Reverse the Rest of the Array**:
   - `[5, 6, 7, 4, 3, 2, 1]` becomes `[5, 6, 7, 1, 2, 3, 4]`.

These approaches efficiently rotate the array to the right by `k` steps. The built-in function approach is more concise, while the non-built-in function approach is more instructive about the underlying mechanics.


leetcode 

/**

* @param {number[]} nums

* @param {number} k

* @return {void} Do not return anything, modify nums in-place instead.

*/

  

function reverse(nums, left, right) {

while (left < right) {

let temp = nums[left];

nums[left++] = nums[right]

nums[right--] = temp

}

}

var rotate = function (nums, k) {

let size = nums.length

k = k % size

  

// use buil in function

// const rotatedArray = nums.splice(size - k, size);

// nums.unshift(...rotatedArray)

  
  

reverse(nums, 0, nums.length - 1)

reverse(nums, 0, k - 1)

reverse(nums, k, nums.length - 1)

  
  

return nums

  

};
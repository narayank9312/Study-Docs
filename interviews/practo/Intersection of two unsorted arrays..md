Find Intersection of two unsorted arrays.

#### You have been given two integer arrays/list(ARR1 and ARR2) of size N and M, respectively. You need to print their intersection; An intersection for this problem can be defined when both the arrays/lists contain a particular value or to put it in other words, when there is a common value that exists in both the arrays/lists.


Ways to make Coin Change

#### You are given an infinite supply of coins of each of denominations D = {D0, D1, D2, D3, ...... Dn-1}. You need to figure out the total number of ways W, in which you can make a change for value V using coins of denominations from D. Print 0, if a change isn't possible.


Longest Substring Without Repeating Characters

#### Given a string 'S' of length 'L', return the length of the longest substring without repeating characters.


Palindrome Linked List

#### You are given a singly Linked List of integers. Your task is to return true if the given singly linked list is a palindrome otherwise returns false.


Search an element in a sorted and rotated array

#### Aahad and Harshit always have fun by solving problems. Harshit took a sorted array and rotated it clockwise by an unknown amount. For example, he took a sorted array = [1, 2, 3, 4, 5] and if he rotates it by 2, then the array becomes: [4, 5, 1, 2, 3].

#### After rotating a sorted array, Aahad needs to answer Q queries asked by Harshit, each of them is described by one integer Q[i]. which Harshit wanted him to search in the array. For each query, if he found it, he had to shout the index of the number, otherwise, he had to shout -1.

#### For each query, you have to complete the given method where 'key' denotes Q[i]. If the key exists in the array, return the index of the 'key', otherwise, return -1.


Balanced parentheses

#### Given an integer ‘N’ representing the number of pairs of parentheses, Find all the possible combinations of balanced parentheses with the given number of pairs of parentheses.

Trapping Rain Water

#### You have been given a long type array/list 'ARR' of size 'N'. It represents an elevation map wherein 'ARR[i]' denotes the elevation of the 'ith' bar. Print the total amount of rainwater that can be trapped in these elevations.


Rotting Oranges

#### You have been given a grid containing some oranges. Each cell of this grid has one of the three integers values:

#### - Value 0 - representing an empty cell.

#### - Value 1 - representing a fresh orange.

#### - Value 2 - representing a rotten orange.

#### Every second, any fresh orange that is adjacent(4-directionally) to a rotten orange becomes rotten.

#### Your task is to find out the minimum time after which no cell has a fresh orange. If it's impossible to rot all the fresh oranges then print -1.



#### Implement a queue data structure which follows FIFO(First In First Out) property, using only the instances of the stack data structure.


Merge Intervals

#### You are given N number of intervals, where each interval contains two integers denoting the start time and the end time for the interval.

#### The task is to merge all the overlapping intervals and return the list of merged intervals sorted by increasing order of their start time.

#### Two intervals [A,B] and [C,D] are said to be overlapping with each other if there is at least one integer that is covered by both of them.

Let's address each of the problems one by one with detailed explanations and JavaScript code examples:

### 1. Find Intersection of Two Unsorted Arrays

**Problem**: Given two integer arrays/lists, print their intersection. The intersection contains common values that exist in both arrays.

**Approach**:
- Use a hash map to store the frequency of elements in the first array.
- Traverse the second array and check if the element exists in the hash map.

**Code**:
```javascript
function findIntersection(arr1, arr2) {
  let map = {};
  let intersection = [];

  // Store elements of arr1 in a map
  for (let num of arr1) {
    if (!map[num]) {
      map[num] = 1;
    } else {
      map[num]++;
    }
  }

  // Find intersections with arr2
  for (let num of arr2) {
    if (map[num] && map[num] > 0) {
      intersection.push(num);
      map[num]--;
    }
  }

  return intersection;
}

// Example usage:
let arr1 = [4, 9, 5];
let arr2 = [9, 4, 9, 8, 4];
console.log(findIntersection(arr1, arr2)); // Output: [4, 9]
```

### 2. Ways to Make Coin Change

**Problem**: Given an infinite supply of coins of denominations, figure out the total number of ways to make change for a value using these denominations.

**Approach**:
- Use dynamic programming to build a table where the value at each index represents the number of ways to make change for that amount.

**Code**:
```javascript
function countWaysToMakeChange(coins, value) {
  let dp = Array(value + 1).fill(0);
  dp[0] = 1; // Base case: one way to make change for zero value

  for (let coin of coins) {
    for (let i = coin; i <= value; i++) {
      dp[i] += dp[i - coin];
    }
  }

  return dp[value];
}

// Example usage:
let coins = [1, 2, 3];
let value = 4;
console.log(countWaysToMakeChange(coins, value)); // Output: 4
```

### 3. Longest Substring Without Repeating Characters

**Problem**: Given a string, return the length of the longest substring without repeating characters.

**Approach**:
- Use the sliding window technique with a hash map to track the last seen positions of characters.

**Code**:
```javascript
function lengthOfLongestSubstring(s) {
  let map = new Map();
  let maxLength = 0;
  let start = 0;

  for (let end = 0; end < s.length; end++) {
    if (map.has(s[end])) {
      start = Math.max(map.get(s[end]) + 1, start);
    }
    map.set(s[end], end);
    maxLength = Math.max(maxLength, end - start + 1);
  }

  return maxLength;
}

// Example usage:
let s = "abcabcbb";
console.log(lengthOfLongestSubstring(s)); // Output: 3
```

### 4. Palindrome Linked List

**Problem**: Given a singly linked list of integers, return true if it is a palindrome.

**Approach**:
- Use a fast and slow pointer to find the middle of the list.
- Reverse the second half of the list.
- Compare the first half and the reversed second half.

**Code**:
```javascript
class ListNode {
  constructor(val) {
    this.val = val;
    this.next = null;
  }
}

function isPalindrome(head) {
  if (!head || !head.next) return true;

  let slow = head, fast = head;

  // Find the middle of the list
  while (fast && fast.next) {
    slow = slow.next;
    fast = fast.next.next;
  }

  // Reverse the second half
  let prev = null;
  while (slow) {
    let next = slow.next;
    slow.next = prev;
    prev = slow;
    slow = next;
  }

  // Compare the two halves
  let left = head, right = prev;
  while (right) {
    if (left.val !== right.val) return false;
    left = left.next;
    right = right.next;
  }

  return true;
}

// Example usage:
let head = new ListNode(1);
head.next = new ListNode(2);
head.next.next = new ListNode(2);
head.next.next.next = new ListNode(1);
console.log(isPalindrome(head)); // Output: true
```

### 5. Search an Element in a Sorted and Rotated Array

**Problem**: Given a sorted array that has been rotated, find the index of a given element.

**Approach**:
- Use binary search to find the element in the rotated array.

**Code**:
```javascript
function searchInRotatedArray(arr, key) {
  let left = 0, right = arr.length - 1;

  while (left <= right) {
    let mid = Math.floor((left + right) / 2);

    if (arr[mid] === key) return mid;

    // Determine which part is sorted
    if (arr[left] <= arr[mid]) {
      if (key >= arr[left] && key < arr[mid]) {
        right = mid - 1;
      } else {
        left = mid + 1;
      }
    } else {
      if (key > arr[mid] && key <= arr[right]) {
        left = mid + 1;
      } else {
        right = mid - 1;
      }
    }
  }

  return -1;
}

// Example usage:
let arr = [4, 5, 6, 7, 0, 1, 2];
let key = 0;
console.log(searchInRotatedArray(arr, key)); // Output: 4
```

### 6. Balanced Parentheses

**Problem**: Given an integer representing the number of pairs of parentheses, find all possible combinations of balanced parentheses.

**Approach**:
- Use recursion and backtracking to generate the combinations.

**Code**:
```javascript
function generateParentheses(n) {
  let result = [];
  function backtrack(s, left, right) {
    if (s.length === 2 * n) {
      result.push(s);
      return;
    }
    if (left < n) {
      backtrack(s + '(', left + 1, right);
    }
    if (right < left) {
      backtrack(s + ')', left, right + 1);
    }
  }
  backtrack('', 0, 0);
  return result;
}

// Example usage:
console.log(generateParentheses(3)); // Output: ["((()))","(()())","(())()","()(())","()()()"]
```

### 7. Trapping Rain Water

**Problem**: Given an array representing elevation map, find the total amount of rainwater that can be trapped.

**Approach**:
- Use two arrays to store the maximum heights from the left and right, then calculate the trapped water.

**Code**:
```javascript
function trapRainWater(heights) {
  if (heights.length === 0) return 0;

  let leftMax = Array(heights.length).fill(0);
  let rightMax = Array(heights.length).fill(0);
  let water = 0;

  leftMax[0] = heights[0];
  for (let i = 1; i < heights.length; i++) {
    leftMax[i] = Math.max(leftMax[i - 1], heights[i]);
  }

  rightMax[heights.length - 1] = heights[heights.length - 1];
  for (let i = heights.length - 2; i >= 0; i--) {
    rightMax[i] = Math.max(rightMax[i + 1], heights[i]);
  }

  for (let i = 0; i < heights.length; i++) {
    water += Math.min(leftMax[i], rightMax[i]) - heights[i];
  }

  return water;
}

// Example usage:
let heights = [0,1,0,2,1,0,1,3,2,1,2,1];
console.log(trapRainWater(heights)); // Output: 6
```

### 8. Rotting Oranges

**Problem**: Given a grid of oranges, find the minimum time to rot all oranges or return -1 if impossible.

**Approach**:
- Use BFS to simulate the rotting process.

**Code**:
```javascript
function orangesRotting(grid) {
  let rows = grid.length;
  let cols = grid[0].length;
  let queue = [];
  let freshCount = 0;

  // Initialize the queue with all rotten oranges and count fresh oranges
  for (let r = 0; r < rows; r++) {
    for (let c = 0; c < cols; c++) {
      if (grid[r][c] === 2) {
        queue.push([r, c]);
      }
      if (grid[r][c] === 1) {
        freshCount++;
      }
    }
  }

  if (freshCount === 0) return 0; // No fresh oranges

  let directions = [[1, 0], [-1, 0], [0, 1], [0, -1]];
  let minutes = 0;

  while (queue.length > 0)

 {
    minutes++;
    let newQueue = [];
    while (queue.length > 0) {
      let [r, c] = queue.shift();
      for (let [dr, dc] of directions) {
        let nr = r + dr, nc = c + dc;
        if (nr >= 0 && nr < rows && nc >= 0 && nc < cols && grid[nr][nc] === 1) {
          grid[nr][nc] = 2;
          freshCount--;
          newQueue.push([nr, nc]);
        }
      }
    }
    queue = newQueue;
  }

  return freshCount === 0 ? minutes - 1 : -1;
}

// Example usage:
let grid = [
  [2, 1, 1],
  [1, 1, 0],
  [0, 1, 1]
];
console.log(orangesRotting(grid)); // Output: 4
```

### 9. Implement a Queue Using Two Stacks

**Problem**: Implement a queue with FIFO property using two stacks.

**Approach**:
- Use two stacks, one for enqueue and one for dequeue operations.

**Code**:
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

  peek() {
    if (this.stack2.length === 0) {
      while (this.stack1.length > 0) {
        this.stack2.push(this.stack1.pop());
      }
    }
    return this.stack2[this.stack2.length - 1];
  }

  isEmpty() {
    return this.stack1.length === 0 && this.stack2.length === 0;
  }
}

// Example usage:
let queue = new Queue();
queue.enqueue(1);
queue.enqueue(2);
console.log(queue.dequeue()); // 1
queue.enqueue(3);
console.log(queue.peek()); // 2
console.log(queue.dequeue()); // 2
console.log(queue.dequeue()); // 3
console.log(queue.isEmpty()); // true
```

### 10. Merge Intervals

**Problem**: Given N intervals, merge all overlapping intervals and return the list of merged intervals sorted by increasing start time.

**Approach**:
- Sort the intervals by the start time.
- Traverse the sorted intervals and merge overlapping intervals.

**Code**:
```javascript
function mergeIntervals(intervals) {
  if (intervals.length === 0) return [];

  intervals.sort((a, b) => a[0] - b[0]);
  let merged = [intervals[0]];

  for (let i = 1; i < intervals.length; i++) {
    let last = merged[merged.length - 1];
    let current = intervals[i];

    if (current[0] <= last[1]) {
      last[1] = Math.max(last[1], current[1]);
    } else {
      merged.push(current);
    }
  }

  return merged;
}

// Example usage:
let intervals = [[1, 3], [2, 6], [8, 10], [15, 18]];
console.log(mergeIntervals(intervals)); // Output: [[1, 6], [8, 10], [15, 18]]
```

By understanding and implementing these solutions, you will be well-prepared to tackle similar problems in an interview setting.
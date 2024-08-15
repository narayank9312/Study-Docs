### Segment Tree for Range Sum Query

A Segment Tree is a data structure used for storing information about intervals or segments. It allows querying which segment contains a given point and is efficient for querying and updating ranges.

### Key Concepts:

1. **Tree Structure**:
   - Each node in the segment tree represents an interval.
   - The root node represents the entire interval.
   - Leaf nodes represent individual elements.

2. **Operations**:
   - **Build**: Construct the tree from an array.
   - **Update**: Update an element and propagate changes up the tree.
   - **Query**: Compute the sum over a range of elements.

### Implementation in JavaScript:

#### Building the Segment Tree:
```javascript
class SegmentTree {
  constructor(arr) {
    this.n = arr.length;
    this.tree = Array(2 * this.n).fill(0);
    this.build(arr);
  }

  build(arr) {
    // Initialize leaves in the tree
    for (let i = 0; i < this.n; i++) {
      this.tree[this.n + i] = arr[i];
    }
    // Build the tree by calculating parents
    for (let i = this.n - 1; i > 0; i--) {
      this.tree[i] = this.tree[2 * i] + this.tree[2 * i + 1];
    }
  }

  update(index, value) {
    // Update the value at the leaf node
    index += this.n;
    this.tree[index] = value;

    // Propagate the changes up to the root
    while (index > 1) {
      index = Math.floor(index / 2);
      this.tree[index] = this.tree[2 * index] + this.tree[2 * index + 1];
    }
  }

  query(left, right) {
    left += this.n;
    right += this.n;
    let sum = 0;

    while (left <= right) {
      if (left % 2 === 1) {
        sum += this.tree[left];
        left++;
      }
      if (right % 2 === 0) {
        sum += this.tree[right];
        right--;
      }
      left = Math.floor(left / 2);
      right = Math.floor(right / 2);
    }

    return sum;
  }
}

// Example usage:
const arr = [1, 2, 3, 4, 5];
const segTree = new SegmentTree(arr);
console.log(segTree.query(1, 3)); // Output: 9 (2 + 3 + 4)
segTree.update(2, 10);
console.log(segTree.query(1, 3)); // Output: 16 (2 + 10 + 4)
```

### Summary:

- **Segment Trees**: Efficiently handle range queries and updates.
- **Build**: Construct the tree from an array in O(n) time.
- **Update**: Modify an element and update the tree in O(log n) time.
- **Query**: Compute the sum of elements in a range in O(log n) time.

Segment trees are particularly useful in scenarios where you need to perform frequent updates and queries on a range of elements, such as in interval scheduling and computational geometry.
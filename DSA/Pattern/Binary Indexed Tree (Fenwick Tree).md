### Binary Indexed Tree (Fenwick Tree)

A Binary Indexed Tree (BIT), also known as a Fenwick Tree, is a data structure that provides efficient methods for calculation and manipulation of prefix sums of a table of values.

### Key Concepts:

1. **Prefix Sum**:
   - Supports point updates and prefix sum queries in logarithmic time.
   
2. **Structure**:
   - Uses a tree-like structure based on binary indexing.

### Operations:

1. **Initialization**:
   - Construct the tree from an array.

2. **Update**:
   - Update an element and propagate changes.

3. **Query**:
   - Calculate the prefix sum up to a given index.

### Implementation in JavaScript:

#### Building and Using a Fenwick Tree:

```javascript
class FenwickTree {
  constructor(size) {
    this.size = size;
    this.tree = Array(size + 1).fill(0);
  }

  update(index, value) {
    while (index <= this.size) {
      this.tree[index] += value;
      index += index & -index;
    }
  }

  query(index) {
    let sum = 0;
    while (index > 0) {
      sum += this.tree[index];
      index -= index & -index;
    }
    return sum;
  }

  build(arr) {
    for (let i = 0; i < arr.length; i++) {
      this.update(i + 1, arr[i]);
    }
  }
}

// Example usage:
const arr = [1, 2, 3, 4, 5];
const fenwickTree = new FenwickTree(arr.length);
fenwickTree.build(arr);
console.log(fenwickTree.query(3)); // Output: 6 (1 + 2 + 3)
fenwickTree.update(3, 2);
console.log(fenwickTree.query(3)); // Output: 8 (1 + 2 + 5)
```

### Summary:

- **Binary Indexed Trees**: Efficiently handle prefix sum queries and updates.
- **Build**: Construct the tree from an array in O(n log n) time.
- **Update**: Modify an element and update the tree in O(log n) time.
- **Query**: Compute the prefix sum in O(log n) time.

Binary Indexed Trees are particularly useful for applications that require frequent updates and prefix sum queries, such as in cumulative frequency tables and computational geometry.
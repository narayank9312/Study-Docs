### Binary Tree

A binary tree is a tree data structure where each node has at most two children, referred to as the left child and the right child.

### Key Concepts:

1. **Node**:
   - Contains a value and pointers to left and right children.

2. **Root**:
   - The top node of the tree.

3. **Leaf**:
   - A node with no children.

### Types of Binary Trees:

1. **Full Binary Tree**:
   - Every node has 0 or 2 children.

2. **Complete Binary Tree**:
   - All levels are completely filled except possibly for the last level, which is filled from left to right.

3. **Perfect Binary Tree**:
   - All internal nodes have two children and all leaf nodes are at the same level.

4. **Balanced Binary Tree**:
   - The height of the two subtrees of any node differ by at most one.

### Implementation in JavaScript:

#### Basic Binary Tree Node and Traversal:

```javascript
class TreeNode {
  constructor(value) {
    this.value = value;
    this.left = null;
    this.right = null;
  }
}

class BinaryTree {
  constructor() {
    this.root = null;
  }

  insert(value) {
    const newNode = new TreeNode(value);
    if (this.root === null) {
      this.root = newNode;
      return;
    }

    let current = this.root;
    while (true) {
      if (value < current.value) {
        if (current.left === null) {
          current.left = newNode;
          return;
        }
        current = current.left;
      } else {
        if (current.right === null) {
          current.right = newNode;
          return;
        }
        current = current.right;
      }
    }
  }

  preOrderTraversal(node = this.root) {
    if (node !== null) {
      console.log(node.value);
      this.preOrderTraversal(node.left);
      this.preOrderTraversal(node.right);
    }
  }

  inOrderTraversal(node = this.root) {
    if (node !== null) {
      this.inOrderTraversal(node.left);
      console.log(node.value);
      this.inOrderTraversal(node.right);
    }
  }

  postOrderTraversal(node = this.root) {
    if (node !== null) {
      this.postOrderTraversal(node.left);
      this.postOrderTraversal(node.right);
      console.log(node.value);
    }
  }
}

// Example usage:
const tree = new BinaryTree();
tree.insert(10);
tree.insert(5);
tree.insert(15);
tree.insert(3);
tree.insert(7);

console.log("Pre-Order Traversal:");
tree.preOrderTraversal(); // Output: 10, 5, 3, 7, 15

console.log("In-Order Traversal:");
tree.inOrderTraversal(); // Output: 3, 5, 7, 10, 15

console.log("Post-Order Traversal:");
tree.postOrderTraversal(); // Output: 3, 7, 5, 15, 10
```

### Summary:

- **Binary Trees**: Data structures where each node has at most two children.
- **Traversals**: Methods to visit all nodes in a tree—pre-order, in-order, and post-order.
- **Types**: Full, complete, perfect, and balanced binary trees.

Binary trees are foundational structures used in various applications, such as expression parsing, search algorithms, and hierarchical data storage.
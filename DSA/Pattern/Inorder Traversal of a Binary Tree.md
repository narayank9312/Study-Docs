### Inorder Traversal of a Binary Tree

Inorder traversal of a binary tree visits nodes in the following order: left subtree, root, and then right subtree. This can be implemented both recursively and iteratively.

### Recursive Inorder Traversal:

```javascript
class TreeNode {
  constructor(value) {
    this.value = value;
    this.left = null;
    this.right = null;
  }
}

function inorderTraversalRecursive(root) {
  const result = [];
  
  function traverse(node) {
    if (!node) return;
    traverse(node.left);
    result.push(node.value);
    traverse(node.right);
  }
  
  traverse(root);
  return result;
}

// Example usage:
const root = new TreeNode(1);
root.right = new TreeNode(2);
root.right.left = new TreeNode(3);

console.log(inorderTraversalRecursive(root)); // Output: [1, 3, 2]
```

### Iterative Inorder Traversal:

```javascript
function inorderTraversalIterative(root) {
  const result = [];
  const stack = [];
  let current = root;
  
  while (current || stack.length > 0) {
    while (current) {
      stack.push(current);
      current = current.left;
    }
    
    current = stack.pop();
    result.push(current.value);
    current = current.right;
  }
  
  return result;
}

// Example usage:
console.log(inorderTraversalIterative(root)); // Output: [1, 3, 2]
```

### Summary:

- **Recursive Inorder Traversal**: Simple to implement, but uses stack space equivalent to the height of the tree.
- **Iterative Inorder Traversal**: Uses an explicit stack to simulate the recursion, suitable for large trees to avoid stack overflow.

These implementations help in understanding the different approaches to inorder traversal in a binary tree.
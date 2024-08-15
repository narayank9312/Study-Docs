### Inverting a Binary Tree

Inverting a binary tree means swapping the left and right children of every node in the tree.

#### Recursive Approach:

```javascript
class TreeNode {
  constructor(value) {
    this.value = value;
    this.left = null;
    this.right = null;
  }
}

function invertTree(root) {
  if (!root) return null;

  const left = invertTree(root.left);
  const right = invertTree(root.right);

  root.left = right;
  root.right = left;

  return root;
}

// Example usage:
const root = new TreeNode(1);
root.left = new TreeNode(2);
root.right = new TreeNode(3);
root.left.left = new TreeNode(4);
root.left.right = new TreeNode(5);

invertTree(root);
// Tree is now inverted
```

#### Iterative Approach:

```javascript
function invertTreeIterative(root) {
  if (!root) return null;

  const stack = [root];

  while (stack.length > 0) {
    const current = stack.pop();

    [current.left, current.right] = [current.right, current.left];

    if (current.left) stack.push(current.left);
    if (current.right) stack.push(current.right);
  }

  return root;
}

// Example usage:
invertTreeIterative(root);
// Tree is now inverted
```

### Reversing a Linked List

Reversing a linked list means changing the next pointers of each node to point to the previous node.

#### Recursive Approach:

```javascript
class ListNode {
  constructor(value) {
    this.value = value;
    this.next = null;
  }
}

function reverseListRecursive(head) {
  if (!head || !head.next) return head;

  const newHead = reverseListRecursive(head.next);
  head.next.next = head;
  head.next = null;

  return newHead;
}

// Example usage:
let head = new ListNode(1);
head.next = new ListNode(2);
head.next.next = new ListNode(3);

head = reverseListRecursive(head);
// Linked list is now reversed
```

#### Iterative Approach:

```javascript
function reverseListIterative(head) {
  let prev = null;
  let current = head;

  while (current) {
    const next = current.next;
    current.next = prev;
    prev = current;
    current = next;
  }

  return prev;
}

// Example usage:
head = reverseListIterative(head);
// Linked list is now reversed
```

### Deep Dive Explanation:

**Inverting a Binary Tree:**
- **Recursive Approach:** The function calls itself on the left and right subtrees, swapping them at each level.
- **Iterative Approach:** Uses a stack to iteratively swap left and right children of each node.

**Reversing a Linked List:**
- **Recursive Approach:** Recursively processes the list and reverses the pointers on the return path.
- **Iterative Approach:** Iteratively changes the pointers using a while loop and temporary variables.

Both tasks involve changing the structure of the data structure (tree or linked list) by modifying pointers or child references. The recursive methods often provide a clearer and more concise solution, while the iterative methods may be more efficient in terms of space complexity.
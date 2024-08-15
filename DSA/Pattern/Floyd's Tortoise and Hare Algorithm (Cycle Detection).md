### Floyd's Tortoise and Hare Algorithm (Cycle Detection)

Floyd’s Tortoise and Hare is an algorithm for detecting cycles in a linked list. It uses two pointers, moving at different speeds to determine if a cycle exists.

### Key Concepts:

1. **Slow and Fast Pointers**:
   - **Slow Pointer (Tortoise)**: Moves one step at a time.
   - **Fast Pointer (Hare)**: Moves two steps at a time.

2. **Cycle Detection**:
   - If there’s a cycle, the fast pointer will eventually meet the slow pointer.
   - If there’s no cycle, the fast pointer will reach the end of the list.

### Code Example:

```javascript
class ListNode {
  constructor(value) {
    this.value = value;
    this.next = null;
  }
}

function hasCycle(head) {
  if (!head || !head.next) return false;

  let slow = head;
  let fast = head;

  while (fast && fast.next) {
    slow = slow.next;
    fast = fast.next.next;

    if (slow === fast) return true;
  }

  return false;
}

// Example usage:
let head = new ListNode(1);
head.next = new ListNode(2);
head.next.next = new ListNode(3);
head.next.next.next = new ListNode(4);
head.next.next.next.next = head.next; // Creates a cycle

console.log(hasCycle(head)); // Output: true
```

### Detailed Flowchart:

**1. Initialization**:
   - Slow pointer at the head.
   - Fast pointer at the head.

**2. Movement**:
   - Move slow pointer one step.
   - Move fast pointer two steps.

**3. Detection**:
   - If slow pointer equals fast pointer, a cycle is detected.
   - If fast pointer reaches the end, no cycle exists.

```plaintext
Initial:
+-------------------------+
| Slow Pointer (head)     |
| Fast Pointer (head)     |
+-------------------------+

Iteration:
+-------------------------+
| Slow Pointer = 1 step   |
| Fast Pointer = 2 steps  |
+-------------------------+

Cycle Detection:
+-------------------------+
| Slow Pointer == Fast    |
| Pointer (Cycle Exists)  |
+-------------------------+
```

This algorithm is efficient with O(n) time complexity and O(1) space complexity, making it suitable for cycle detection in linked lists.
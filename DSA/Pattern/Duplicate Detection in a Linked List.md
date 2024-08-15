### Duplicate Detection in a Linked List

**Concept**: Detect if a linked list contains duplicates.
**Approach**:
1. **Using a Set**:
   - Traverse the list and store each element in a set.
   - If an element is already in the set, a duplicate is detected.

**Implementation**:
```javascript
class ListNode {
  constructor(value) {
    this.value = value;
    this.next = null;
  }
}

function hasDuplicate(head) {
  const seen = new Set();
  let current = head;

  while (current) {
    if (seen.has(current.value)) {
      return true; // Duplicate found
    }
    seen.add(current.value);
    current = current.next;
  }

  return false; // No duplicates
}

// Example usage:
const head = new ListNode(1);
head.next = new ListNode(2);
head.next.next = new ListNode(3);
head.next.next.next = new ListNode(2);

console.log(hasDuplicate(head)); // Output: true
```

### Loop Detection in a Linked List

**Concept**: Detect if a linked list contains a cycle (loop).
**Approach**:
1. **Floyd’s Tortoise and Hare Algorithm**:
   - Use two pointers, a slow pointer (moves one step) and a fast pointer (moves two steps).
   - If they meet, there is a cycle.

**Implementation**:
```javascript
function hasCycle(head) {
  if (!head || !head.next) return false;

  let slow = head;
  let fast = head;

  while (fast && fast.next) {
    slow = slow.next;
    fast = fast.next.next;

    if (slow === fast) {
      return true; // Cycle found
    }
  }

  return false; // No cycle
}

// Example usage:
const node1 = new ListNode(1);
const node2 = new ListNode(2);
const node3 = new ListNode(3);
const node4 = new ListNode(4);

node1.next = node2;
node2.next = node3;
node3.next = node4;
node4.next = node2; // Creates a cycle

console.log(hasCycle(node1)); // Output: true
```

### Summary:

- **Duplicate Detection**: Use a set to track seen values.
- **Loop Detection**: Use Floyd’s Tortoise and Hare algorithm to detect cycles.

Both methods efficiently solve their respective problems in linear time and constant space, making them suitable for large linked lists.
### Heaps and Priority Queues

A heap is a specialized tree-based data structure that satisfies the heap property. Heaps are commonly used to implement priority queues, which allow efficient retrieval of the highest (or lowest) priority element.

### Key Concepts:

1. **Heap Property**:
   - **Max-Heap**: The value of each node is greater than or equal to the values of its children. The largest element is at the root.
   - **Min-Heap**: The value of each node is less than or equal to the values of its children. The smallest element is at the root.

2. **Complete Binary Tree**:
   - Heaps are complete binary trees, meaning all levels are fully filled except possibly the last level, which is filled from left to right.

### Operations:

1. **Insertion**:
   - Add the new element at the end of the heap.
   - Heapify up: Compare with its parent and swap if necessary, repeating until the heap property is restored.

2. **Deletion**:
   - Remove the root element (highest or lowest priority).
   - Move the last element to the root and heapify down: Compare with its children and swap if necessary, repeating until the heap property is restored.

### Implementation in JavaScript:

#### Min-Heap Example:
```javascript
class MinHeap {
  constructor() {
    this.heap = [];
  }

  getParentIndex(index) {
    return Math.floor((index - 1) / 2);
  }

  getLeftChildIndex(index) {
    return 2 * index + 1;
  }

  getRightChildIndex(index) {
    return 2 * index + 2;
  }

  swap(index1, index2) {
    [this.heap[index1], this.heap[index2]] = [this.heap[index2], this.heap[index1]];
  }

  insert(value) {
    this.heap.push(value);
    this.heapifyUp();
  }

  heapifyUp() {
    let index = this.heap.length - 1;
    while (this.getParentIndex(index) >= 0 && this.heap[this.getParentIndex(index)] > this.heap[index]) {
      this.swap(this.getParentIndex(index), index);
      index = this.getParentIndex(index);
    }
  }

  extractMin() {
    if (this.heap.length === 0) return null;
    if (this.heap.length === 1) return this.heap.pop();
    const root = this.heap[0];
    this.heap[0] = this.heap.pop();
    this.heapifyDown();
    return root;
  }

  heapifyDown() {
    let index = 0;
    while (this.getLeftChildIndex(index) < this.heap.length) {
      let smallerChildIndex = this.getLeftChildIndex(index);
      if (this.getRightChildIndex(index) < this.heap.length && this.heap[this.getRightChildIndex(index)] < this.heap[smallerChildIndex]) {
        smallerChildIndex = this.getRightChildIndex(index);
      }
      if (this.heap[index] <= this.heap[smallerChildIndex]) break;
      this.swap(index, smallerChildIndex);
      index = smallerChildIndex;
    }
  }
}

// Example usage:
const minHeap = new MinHeap();
minHeap.insert(3);
minHeap.insert(1);
minHeap.insert(6);
minHeap.insert(5);
minHeap.insert(2);
minHeap.insert(4);
console.log(minHeap.extractMin()); // Output: 1
console.log(minHeap.extractMin()); // Output: 2
```

### Priority Queue

A priority queue is an abstract data type similar to a regular queue but with an added feature of associating a priority with each element. Elements are dequeued based on their priority, not just their insertion order.

#### Priority Queue Using Min-Heap:
```javascript
class PriorityQueue {
  constructor() {
    this.heap = new MinHeap();
  }

  enqueue(value) {
    this.heap.insert(value);
  }

  dequeue() {
    return this.heap.extractMin();
  }

  isEmpty() {
    return this.heap.length === 0;
  }
}

// Example usage:
const pq = new PriorityQueue();
pq.enqueue(5);
pq.enqueue(2);
pq.enqueue(8);
pq.enqueue(1);
console.log(pq.dequeue()); // Output: 1
console.log(pq.dequeue()); // Output: 2
```

### Summary:

- **Heaps**: Efficiently manage a collection of elements with a priority, supporting operations like insertion and deletion.
- **Priority Queues**: Use heaps to maintain and retrieve elements based on their priority.
- **Applications**: Used in algorithms like Dijkstra's shortest path, heapsort, and task scheduling.
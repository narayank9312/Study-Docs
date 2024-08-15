### Depth First Search (DFS) Algorithm

Depth First Search (DFS) is an algorithm for traversing or searching tree or graph data structures. The algorithm starts at the root (or an arbitrary node in the case of a graph) and explores as far as possible along each branch before backtracking.

### Key Concepts:

1. **Traversal**:
   - **Preorder**: Visit the node first, then recursively visit the left and right subtrees.
   - **Inorder**: Recursively visit the left subtree, visit the node, then the right subtree.
   - **Postorder**: Recursively visit the left and right subtrees, then visit the node.

2. **Backtracking**:
   - When there are no more nodes to explore, the algorithm backtracks to the previous node to explore new paths.

### Implementation in JavaScript:

#### DFS for a Tree:
```javascript
class TreeNode {
  constructor(value) {
    this.value = value;
    this.left = null;
    this.right = null;
  }
}

function dfsPreOrder(node) {
  if (node === null) return;
  console.log(node.value);
  dfsPreOrder(node.left);
  dfsPreOrder(node.right);
}

// Example usage:
const root = new TreeNode(1);
root.left = new TreeNode(2);
root.right = new TreeNode(3);
root.left.left = new TreeNode(4);
root.left.right = new TreeNode(5);

dfsPreOrder(root); // Output: 1, 2, 4, 5, 3
```

#### DFS for a Graph:
```javascript
class Graph {
  constructor() {
    this.adjacencyList = {};
  }

  addVertex(vertex) {
    if (!this.adjacencyList[vertex]) this.adjacencyList[vertex] = [];
  }

  addEdge(vertex1, vertex2) {
    this.adjacencyList[vertex1].push(vertex2);
    this.adjacencyList[vertex2].push(vertex1);
  }

  dfs(start) {
    const result = [];
    const visited = {};
    const adjacencyList = this.adjacencyList;

    (function dfsHelper(vertex) {
      if (!vertex) return null;
      visited[vertex] = true;
      result.push(vertex);

      adjacencyList[vertex].forEach(neighbor => {
        if (!visited[neighbor]) {
          return dfsHelper(neighbor);
        }
      });
    })(start);

    return result;
  }
}

// Example usage:
const graph = new Graph();
graph.addVertex("A");
graph.addVertex("B");
graph.addVertex("C");
graph.addVertex("D");
graph.addVertex("E");
graph.addVertex("F");

graph.addEdge("A", "B");
graph.addEdge("A", "C");
graph.addEdge("B", "D");
graph.addEdge("C", "E");
graph.addEdge("D", "E");
graph.addEdge("D", "F");
graph.addEdge("E", "F");

console.log(graph.dfs("A")); // Output: [ 'A', 'B', 'D', 'E', 'C', 'F' ]
```

### Flowchart:

**1. DFS for Tree (Preorder Traversal)**:
```plaintext
                1
              /   \
            2       3
          /   \
         4     5

DFS Preorder:
- Visit 1
- Visit 2
- Visit 4
- Backtrack to 2
- Visit 5
- Backtrack to 1
- Visit 3
```

**2. DFS for Graph**:
```plaintext
  A - B - D
  |   |   |
  C - E - F

Start from A:
- Visit A
- Visit B
- Visit D
- Visit E
- Visit C
- Visit F
```

### Summary:

- **DFS** explores as far as possible along each branch before backtracking.
- **Tree Traversal** can be done in preorder, inorder, or postorder.
- **Graph Traversal** involves visiting nodes, marking them as visited, and using recursion or a stack to explore neighbors.
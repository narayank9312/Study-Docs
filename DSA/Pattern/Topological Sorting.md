### Topological Sorting

Topological sorting of a Directed Acyclic Graph (DAG) is a linear ordering of its vertices such that for every directed edge `u -> v`, vertex `u` comes before `v` in the ordering.

### Key Concepts:

1. **Directed Acyclic Graph (DAG)**:
   - A graph with directed edges and no cycles.

2. **Linear Ordering**:
   - A sequence where each directed edge’s start vertex precedes its end vertex.

### Algorithms:

1. **Kahn's Algorithm (BFS-Based)**:
   - Uses in-degree of vertices.
   - Repeatedly removes nodes with zero in-degree.

2. **Depth-First Search (DFS-Based)**:
   - Uses recursion.
   - Adds vertices to the stack in post-order.

### Implementation in JavaScript:

#### Kahn's Algorithm:

```javascript
function topologicalSortKahn(graph) {
  const inDegree = Array(graph.length).fill(0);
  const queue = [];
  const topoOrder = [];

  // Compute in-degrees of all vertices
  for (let i = 0; i < graph.length; i++) {
    for (let neighbor of graph[i]) {
      inDegree[neighbor]++;
    }
  }

  // Add all vertices with 0 in-degree to the queue
  for (let i = 0; i < inDegree.length; i++) {
    if (inDegree[i] === 0) {
      queue.push(i);
    }
  }

  // Process the queue
  while (queue.length > 0) {
    const current = queue.shift();
    topoOrder.push(current);

    for (let neighbor of graph[current]) {
      inDegree[neighbor]--;
      if (inDegree[neighbor] === 0) {
        queue.push(neighbor);
      }
    }
  }

  // Check if topological sorting is possible
  if (topoOrder.length !== graph.length) {
    throw new Error("Graph has a cycle, topological sorting not possible.");
  }

  return topoOrder;
}

// Example usage:
const graph = [
  [1, 2], // 0 -> 1, 0 -> 2
  [3],    // 1 -> 3
  [3],    // 2 -> 3
  []      // 3 has no outgoing edges
];
console.log(topologicalSortKahn(graph)); // Output: [0, 1, 2, 3]
```

#### DFS-Based Algorithm:

```javascript
function topologicalSortDFS(graph) {
  const visited = Array(graph.length).fill(false);
  const stack = [];

  function dfs(node) {
    visited[node] = true;
    for (let neighbor of graph[node]) {
      if (!visited[neighbor]) {
        dfs(neighbor);
      }
    }
    stack.push(node);
  }

  for (let i = 0; i < graph.length; i++) {
    if (!visited[i]) {
      dfs(i);
    }
  }

  return stack.reverse();
}

// Example usage:
console.log(topologicalSortDFS(graph)); // Output: [0, 2, 1, 3]
```

### Summary:

- **Topological Sorting**: Linear ordering of vertices in a DAG.
- **Kahn's Algorithm**: Uses BFS and in-degrees.
- **DFS-Based Algorithm**: Uses post-order traversal.

Topological sorting is used in scheduling tasks, resolving symbol dependencies in linkers, and more.
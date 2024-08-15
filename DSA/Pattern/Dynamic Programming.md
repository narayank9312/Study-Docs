### Dynamic Programming

Dynamic programming (DP) is a method for solving complex problems by breaking them down into simpler subproblems. It is used when the problem can be divided into overlapping subproblems that can be solved independently. DP is particularly useful for optimization problems.

### Key Concepts:

1. **Overlapping Subproblems**:
   - The problem can be broken down into smaller, repeating subproblems.

2. **Optimal Substructure**:
   - An optimal solution to the problem contains optimal solutions to its subproblems.

3. **Memoization**:
   - Store results of subproblems to avoid redundant computations.

4. **Tabulation**:
   - Iteratively solve subproblems and store their results in a table (array).

### Implementation in JavaScript:

#### Example 1: Fibonacci Sequence (Memoization)
```javascript
function fibonacci(n, memo = {}) {
  if (n in memo) return memo[n];
  if (n <= 2) return 1;
  memo[n] = fibonacci(n - 1, memo) + fibonacci(n - 2, memo);
  return memo[n];
}

// Example usage:
console.log(fibonacci(10)); // Output: 55
```

#### Example 2: Fibonacci Sequence (Tabulation)
```javascript
function fibonacci(n) {
  if (n <= 2) return 1;
  const fib = [0, 1, 1];
  for (let i = 3; i <= n; i++) {
    fib[i] = fib[i - 1] + fib[i - 2];
  }
  return fib[n];
}

// Example usage:
console.log(fibonacci(10)); // Output: 55
```

#### Example 3: 0/1 Knapsack Problem
```javascript
function knapsack(weights, values, capacity) {
  const n = weights.length;
  const dp = Array(n + 1).fill(null).map(() => Array(capacity + 1).fill(0));

  for (let i = 1; i <= n; i++) {
    for (let w = 0; w <= capacity; w++) {
      if (weights[i - 1] <= w) {
        dp[i][w] = Math.max(values[i - 1] + dp[i - 1][w - weights[i - 1]], dp[i - 1][w]);
      } else {
        dp[i][w] = dp[i - 1][w];
      }
    }
  }

  return dp[n][capacity];
}

// Example usage:
const weights = [1, 3, 4, 5];
const values = [1, 4, 5, 7];
const capacity = 7;
console.log(knapsack(weights, values, capacity)); // Output: 9
```

### Flowchart:

**Fibonacci Sequence (Memoization)**
1. **Base Case**: If `n <= 2`, return 1.
2. **Memoization Check**: If result is in memo, return it.
3. **Recursive Call**: Compute `fibonacci(n - 1) + fibonacci(n - 2)` and store in memo.

```plaintext
n = 10
|__ fibonacci(9)
    |__ fibonacci(8)
        |__ ...
        |__ fibonacci(2) -> 1
    |__ fibonacci(1) -> 1
```

**0/1 Knapsack Problem**
1. **Initialize DP Table**: `dp[i][w]` to store max value for first `i` items with weight limit `w`.
2. **Fill DP Table**:
   - For each item `i` and weight `w`, update `dp[i][w]` based on inclusion/exclusion of item.

```plaintext
weights = [1, 3, 4, 5]
values = [1, 4, 5, 7]
capacity = 7

DP Table:
+---+---+---+---+---+---+---+---+
|   | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 |
+---+---+---+---+---+---+---+---+---+
| 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| 1 | 0 | 1 | 1 | 1 | 1 | 1 | 1 | 1 |
| 2 | 0 | 1 | 1 | 4 | 5 | 5 | 5 | 5 |
| 3 | 0 | 1 | 1 | 4 | 5 | 6 | 7 | 9 |
| 4 | 0 | 1 | 1 | 4 | 5 | 6 | 7 | 9 |
+---+---+---+---+---+---+---+---+---+
```

Dynamic programming simplifies solving complex problems by breaking them down into simpler subproblems and storing their solutions to avoid redundant work. This approach is especially useful in optimization problems like the 0/1 Knapsack Problem, shortest paths in graphs, and more.
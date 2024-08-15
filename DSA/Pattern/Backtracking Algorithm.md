### Backtracking Algorithm

Backtracking is a systematic way to iterate through all possible configurations of a search space. It is used to solve problems that can be broken down into a sequence of subproblems, each of which can be solved independently.

### Key Concepts:

1. **Recursive Exploration**:
   - Explore all possible solutions recursively, one step at a time.
   - If a solution does not work, backtrack and try another path.

2. **Base Case**:
   - A condition that stops the recursion when a solution is found or all possibilities are exhausted.

3. **Constraint Checking**:
   - Check constraints at each step to ensure partial solutions can lead to a valid solution.

### Implementation in JavaScript:

#### Example 1: Solving the N-Queens Problem
```javascript
function solveNQueens(n) {
  const result = [];
  const board = Array.from({ length: n }, () => Array(n).fill('.'));
  
  function isSafe(row, col) {
    for (let i = 0; i < row; i++) {
      if (board[i][col] === 'Q') return false;
      if (col - (row - i) >= 0 && board[i][col - (row - i)] === 'Q') return false;
      if (col + (row - i) < n && board[i][col + (row - i)] === 'Q') return false;
    }
    return true;
  }
  
  function backtrack(row = 0) {
    if (row === n) {
      result.push(board.map(r => r.join('')));
      return;
    }
    for (let col = 0; col < n; col++) {
      if (isSafe(row, col)) {
        board[row][col] = 'Q';
        backtrack(row + 1);
        board[row][col] = '.';
      }
    }
  }
  
  backtrack();
  return result;
}

// Example usage:
console.log(solveNQueens(4));
```

#### Example 2: Subset Sum Problem
```javascript
function subsetSum(arr, target) {
  const result = [];
  
  function backtrack(start = 0, currentSum = 0, subset = []) {
    if (currentSum === target) {
      result.push([...subset]);
      return;
    }
    if (currentSum > target) return;
    
    for (let i = start; i < arr.length; i++) {
      subset.push(arr[i]);
      backtrack(i + 1, currentSum + arr[i], subset);
      subset.pop();
    }
  }
  
  backtrack();
  return result;
}

// Example usage:
console.log(subsetSum([2, 3, 6, 7], 7)); // Output: [[7], [2, 3, 2]]
```

### Flowchart:

**1. N-Queens Problem**:
1. **Initialize**:
   - Create an empty board.
2. **Recursive Exploration**:
   - Place a queen in a valid position in the current row.
   - Recursively try to place queens in the subsequent rows.
3. **Backtrack**:
   - If placing the queen leads to a conflict, remove it and try the next position.

**2. Subset Sum Problem**:
1. **Initialize**:
   - Start with an empty subset and sum.
2. **Recursive Exploration**:
   - Add an element to the subset.
   - Recursively check if the subset sum equals the target.
3. **Backtrack**:
   - If the sum exceeds the target, remove the last element and try the next.

```plaintext
N-Queens Problem:
1. Place a queen in a row.
2. Check if it's safe.
3. Move to the next row.
4. Backtrack if conflict arises.

Subset Sum Problem:
1. Add element to subset.
2. Check if subset sum equals target.
3. Move to the next element.
4. Backtrack if sum exceeds target.
```

By using these principles, backtracking efficiently explores all possible solutions for problems like N-Queens, subset sum, and more.
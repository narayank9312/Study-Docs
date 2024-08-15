### Greedy Algorithm

Greedy algorithms build up a solution piece by piece, always choosing the next piece that offers the most immediate benefit. They are used to solve optimization problems and can produce optimal solutions for some problems but not all.

### Key Concepts:

1. **Greedy Choice Property**:
   - Make the locally optimal choice at each step with the hope of finding the global optimum.

2. **Optimal Substructure**:
   - A problem has optimal substructure if an optimal solution to the problem contains optimal solutions to the subproblems.

### Common Problems:

1. **Activity Selection**:
   - Select the maximum number of activities that don't overlap.
   
2. **Fractional Knapsack**:
   - Maximize the total value in the knapsack by taking fractions of items.

3. **Huffman Coding**:
   - Minimize the average code length used for representing a set of symbols.

### Implementation in JavaScript:

#### Example 1: Activity Selection
```javascript
function activitySelection(start, end) {
  const n = start.length;
  let selectedActivities = [];

  let i = 0;
  selectedActivities.push(i);

  for (let j = 1; j < n; j++) {
    if (start[j] >= end[i]) {
      selectedActivities.push(j);
      i = j;
    }
  }

  return selectedActivities;
}

// Example usage:
const start = [1, 3, 0, 5, 8, 5];
const end = [2, 4, 6, 7, 9, 9];
console.log(activitySelection(start, end)); // Output: [0, 1, 3, 4]
```

#### Example 2: Fractional Knapsack
```javascript
class Item {
  constructor(value, weight) {
    this.value = value;
    this.weight = weight;
  }
}

function fractionalKnapsack(capacity, items) {
  items.sort((a, b) => (b.value / b.weight) - (a.value / a.weight));

  let totalValue = 0;
  for (let item of items) {
    if (capacity >= item.weight) {
      capacity -= item.weight;
      totalValue += item.value;
    } else {
      totalValue += (item.value / item.weight) * capacity;
      break;
    }
  }

  return totalValue;
}

// Example usage:
const items = [new Item(60, 10), new Item(100, 20), new Item(120, 30)];
const capacity = 50;
console.log(fractionalKnapsack(capacity, items)); // Output: 240
```

### Flowchart:

**Activity Selection**:
1. **Sort activities** by their finish times.
2. **Select** the first activity.
3. For each subsequent activity, if it starts after or when the last selected activity ends, select it.

**Fractional Knapsack**:
1. **Sort items** by their value-to-weight ratio.
2. **Iterate through items**, adding as much of each item as possible to the knapsack.
3. If the knapsack is filled, calculate the fractional value of the remaining capacity and add it.

```plaintext
Activity Selection:
1. Sort activities by end time
2. Select activity 0
3. For each activity j:
   If start[j] >= end[i], select activity j, set i = j

Fractional Knapsack:
1. Sort items by value/weight
2. For each item:
   If capacity >= item.weight:
     Take full item, decrease capacity
   Else:
     Take fraction of item, fill knapsack, break
```

These examples and concepts illustrate the fundamental approach of greedy algorithms to solve optimization problems efficiently by making locally optimal choices at each step.
### Trees and Prefix Trees (Tries)

#### Trees

A tree is a hierarchical data structure consisting of nodes, with a single node as the root and other nodes as children. Each node contains a value and references to its children. Trees are used to represent hierarchical relationships, such as file systems or organizational structures.

#### Key Concepts:
- **Root**: The top node.
- **Parent/Child**: Nodes connected in the hierarchy.
- **Leaf**: A node with no children.
- **Subtree**: A tree consisting of a node and its descendants.

#### Example:
```plaintext
        A
       / \
      B   C
     / \   \
    D   E   F
```

### Prefix Trees (Tries)

A prefix tree, or trie, is a specialized tree used to store associative data structures. A common application of tries is to store a predictive text or autocomplete dictionary.

#### Key Concepts:
- **Node**: Represents a character of the string.
- **Edge**: Represents the connection between characters.
- **Root**: Represents the start of the trie.
- **End of Word Marker**: Indicates the end of a valid word.

#### Example:
```plaintext
              root
             /    \
            a      b
           / \      \
          p   t      a
         /     \      \
        p       e      t
       /         \      \
      l           r      s
     /             \
    e               r
```

#### Implementation in JavaScript:

**Tree Example**:
```javascript
class TreeNode {
  constructor(value) {
    this.value = value;
    this.children = [];
  }
  
  addChild(child) {
    this.children.push(child);
  }
}

// Example usage:
const root = new TreeNode('A');
const nodeB = new TreeNode('B');
const nodeC = new TreeNode('C');
root.addChild(nodeB);
root.addChild(nodeC);
```

**Trie Example**:
```javascript
class TrieNode {
  constructor() {
    this.children = {};
    this.isEndOfWord = false;
  }
}

class Trie {
  constructor() {
    this.root = new TrieNode();
  }
  
  insert(word) {
    let node = this.root;
    for (let char of word) {
      if (!node.children[char]) {
        node.children[char] = new TrieNode();
      }
      node = node.children[char];
    }
    node.isEndOfWord = true;
  }
  
  search(word) {
    let node = this.root;
    for (let char of word) {
      if (!node.children[char]) {
        return false;
      }
      node = node.children[char];
    }
    return node.isEndOfWord;
  }
}

// Example usage:
const trie = new Trie();
trie.insert('apple');
console.log(trie.search('apple')); // Output: true
console.log(trie.search('app')); // Output: false
```

### Summary:

- **Trees**: Used to represent hierarchical data. Nodes contain values and references to children.
- **Tries**: Specialized trees used to store strings. Efficient for prefix-based searches.

Both data structures are fundamental in computer science, with a variety of applications from file systems to autocomplete functionality.
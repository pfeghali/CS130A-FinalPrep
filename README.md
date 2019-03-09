---
Peter Feghali @ Winter 2019
UCSB `CS130A` Final Study Guide
---
#### Introduction:
This is an incomplete final study guide.
There is probably material missing from here, albeit most information should be valid.
Do not expect substantive proofs, that's not what this is for.
Please email me if you'd like something updated or changed.
---
##### *All code blocks are mine's unless otherwise noted, and might have errors/be suboptimal. I prefer python to C++, and I will be using pseudocode. This will also NOT cover probability and amortized analysis. Other documents and references will be linked to, and a substantive amount of material has been derived from the [course's site](https://www.cs.ucsb.edu/~suri/cs130a/cs130a.html).*
---
# Data Structures and Algorithms
## What is a data structure?
## Worst case bounding (BigO)
## Space Complexities
## Useful series expansions
## Useful complexities
![equation](https://latex.codecogs.com/gif.latex?10x)
# Hashing
## Dictionaries
## Hash table operations
## Collisions & Resolving them
## Choosing a hash function
## Randomization
## Universal hash functions
## Birthday paradox (in a lazy form)
## Perfect hashing
# Priority Queues
## Why?
## Available operations
## How can we represent this?
## Heap-ordered binary trees
### ^?
### Calculating the height
### What is a 'complete tree'?
### Heap property
### Percolate Up
### Percolate Down
### Insert
### DeleteMin (or potentially max!)
### Binary Heap -> Array Representation
## HeapSort
## Build Heap in O(N)
# d-Heaps and Leftist Heaps
## What is a D-Heap?
### Operations
### Complexity
## Leftist Heap
### Why?
### Null Path Length (NPL)
### Operations
### Merge
# Search Trees
## Operations & Complexities
## Traversal
#### PreOrder Traversal
#### PostOrder Traversal
## Binary Search Trees
### Properties
### Operations
### How does insert(e) work?
### How does delete(e) work?
#### e is a leaf
#### e has one child
#### e has two children
### Other details
# Balanced Search Trees
## Why?
## AVL Trees
### Why?
### How? (AVL rules)
### Height properties
### Tree Rotations
#### Why?
#### Single Rotations
##### When?
##### How?
#### Double Rotations?
##### When?
##### How?
### Removal
### Complexity Bounds
# Splay Trees
## Why?
## Splaying
### Zig
### Zig-Zig
### Zig-Zag
## Access
## Join
## Split
## Insert
## Delete
# Amortized Analysis
## Why?
## Aggregate Method
## Accounting Method
## Potential Method
# Graphs
## What's a graph?
### Vertices
### Edges
### Directed vs Undirected
## Examples
## Representations of graphs
## Paths
## Minimally Connect Graph = Tree
## ST Connectivity
## Connected Components
## Breadth First Search (BFS)
## Depth First Search (DFS)
## BiPartititeness
### N-Colorable
## Bi-Connectivity
### Why?
### Articulation Point
## Topological Sort
### Why?
### Forming a topological ordering
## Strong Bi-Connectivity
# Applications of DFS
# Union Find Data Structure
## Background
### A set of sets
## Basic Operations
## Quick Find
## Quick Union
## Smart Union
### Why does this work?
## Path Compression
## Inverse Ackermann
# Mininum Spanning trees
## Why?
## Requirements
## Cut Theorem & Greedy Algorithms
## Prim's Algorithm
## Kruskal's Algorithm
# Shortest Path
## Structural Properties
## Djkstra
### Some quotations of his on lecture slides which are fun
### Algorithm
## Acylcic Graphs
## Bellman Ford
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
A data strcuture is some sort of form which holds data in a (usually) intelligent manner. DS allow for optimized operations on data, and usually are built to have strong bounds on worst case complexity. DS are fundementally important to CS, since the movement, access, analysis, and computation based on data is a lot of what CS is.
## Worst case bounding (BigO)
When we're building a data strucutre, we want to have strcutures which allow for fast operations with millions of elements. We can analyze how something will scale using BigO analysis.  
For example, consider: ![equation](https://latex.codecogs.com/gif.latex?10x^2&plus;5x-34\rightarrow&space;O(N^2)). With BigO analsis we ignore all extranneous coeffecients, and just argue that the function scales according to N^2.
### What about Big\omega?
Big\omega is a representation of the lower bound of a function as N approaches infinity. We can also consider BigO as the upper bound of such a function as N approaches infinity. This usually is not very interesting.
### And Big\theta?
This one is pretty interesting. Big\theta represents some sort of a function that not only represents the upper bound of the algorithm, but also the lower bound. Note, in all of these cases, we care about the general form, and are assuming that there is some sort of coeffecient which is then being multiplied to said functions. Big\theta notation is present when functions such as mergesort come into play. No matter how the algorithm runs, mergesort obeys a consistent set of operations and therefore we can claim that it runs in a Big\theta sort of way.
## Space Complexities
You have a program that's running, and it needs to store data while running. How much does it need (other than the input)? Does it need to store extraneous data for each element? O(N). Does it need to store linkage information between every single element and every other element in the input? O(N^2).
## Useful series expansions
## Useful complexities
<!-- ![equation](https://latex.codecogs.com/gif.latex?10x)-->
# Hashing
Hashing is one of the most useful processes in Computer Science. Need to sort an arbitarily long string of input? Or how about find a substring in O(N)? Store tons of user data easily? Hashtables are generally just great ways to manipulate, store, and interact with data. They're not perfect though.
Just as a general note, picking a relatively prime table size is usually optimal.
## Dictionaries
A dictionary is simply a DS which stores key-value pairs. A key being some sort of accessor, and the value being the value/meaning associated with said accessor. For language, this is a dictionary. Words are the keys, and defintions are the values. 
## Hash table operations
Hash tables support a number of common operations in (near) O(1) time:
1. Lookup
2. Insert
3. Delete

So we have a thing that can do these operations, technically, all the operations are worst case O(n) using non-perfect hashing. Albeit, most of the time, these operations are O(1).

## Collisions & Resolving them
Let's say we hash one thing using a hash function to a certail slot. Due to the pigeonhole principle (n pigeons, n - x slots, more than 1 pigeon must be in at least 1 slot), we will have collisions. How can we deal with this redundancy?
### Probing
Probing is a method of dealing with collisions by moving a number of spaces from a collision. Let us imagine that a collision occurs at a position of 5, with linear probing, we'd continue to check for any free spots following according to some sort of rule. With linear probing, check every n spots, quadratic probing check h(x) + 1, then h(x) + 4, etc...
### Double Hashing
Double hashing has a similair approach to probing, but rather than probing based off of some sort of a defined rule, probe based on a secondary hash function. Not going to go into this.
### Problems with previous approaches
These previous approaches really suck due to 
1. Deletion
2. Size management

#### Deletion
Deletion is a massive problem with the previous two tables. If we insert 3 elements which all hash to slot i, then delete the 2nd element, we have an element at position z which is now harder to reach. To get from i to z, we must take into consideration that the 2nd element's slot had an element in it at some point, which makes searching within the table a serious problem.
#### Size management
With this table approach, ourtable size can reach a maximum. If the table fills, finding a free spot can be hard, and if one is not available, a heurestic must be designed to deal with this constraint. If a slot is not available, common techniques are to increase the table size to the next available prime, then reinsert every element back into said table. This is simply ineffecient, and a pain to have to deal with.
### Chained Hashing
Chained hashing attempts to solve these problems by accepting collisions and just adding elements to the end of some sort of a list as they collide. This approach allows for elemeents to be easily inserted without worrying about trying to find a valid slot. This approach isn't perfect, as if n eleents all hash to slot i, then access is O(N). Albeit, same issue as the other approaches, but now we can make insert consistently O(1).
## Choosing a hash function
Selecting a hash function is a hard problem, as for any preselected hash function we need to minimize a user finding a hash function which will cause an adversial set of elements to hash to the same location. In addition, hash functions must consistently distribute elements evenly across table sizes. Since for any set function we can easily form any type of adversial set, we must somehow manage to remove this possibility.
## Randomization
What if rather than having a set hash function, we have a hash function that even the programmer does not know until table initialization? By allowing for hash function randomization, we can have consistent tables without worrying about a user preselecting an adversial set of inputs.
## Universal hash functions
Such random hash functions are known as universal hash functions, and are defined in the form ![equation](https://latex.codecogs.com/gif.latex?h(x)&space;=&space;rand(m\in&space;\{1,...,M-1\})*x_1&plus;...&plus;rand(m\in&space;\{1,...,M-1\})*x_n)
These hash functions can be proven to have collisions at a rate of 1/M, with M being the table size. Great!
## Matrix method
Rather than choosing integer coeffecients, we can also choose a random binary matrix, of size b\*u, with b being the coeffecient of the table size (M = 2^b) and u being the number of bits in the input. This method s similar to the last, where we take this new hash 'function' and is of the same linearly multiplicative form.
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
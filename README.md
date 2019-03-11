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
What's the likelihood we get a collision in a hash table? Pretty much the same question as asking if we hae n people in a room, what is the likelihood two people have the same birthday? Turns out there's a high probability. For the second person 1/365, then assuming no collision, 2/365, 3/365, etc...
### Stirling's approximation
![equation](https://wikimedia.org/api/rest_v1/media/math/render/svg/7fe20ccef4b13b2fc2b79b752fb595da6d855de2)
## Perfect hashing
So hash tables aren't perfect, we don't get O(1) access all the time. How can we fix that? Perfect hashing is a method built on essentially just having a hashtable of hashtables, and if any one gets too full, rehash it. Proven to be O(1).
1. Hash keys using universal hashing, table of size n.
2. Very likely this will produce some collisions. 
3. Rehash each, but now with a quadratic size hash table.

This may seem like a solution with N^2 space complexity, but it is a O(N) space solution.

# Priority Queues
## Why?
Sometimes we need to know what is next in some sort of an ordering. Imagine some sort of a scheduler, or trying to get the absolute minimum element from sort of continuously fed DS. Doesn't matter, what does matter, is that you have some set ordering rule, and you want to get the thing that obeys said rule the most in order.
## Available operations
Always
- `void insert(e)`
- `e deleteMin()` / `e deleteMax()`

Sometimes:
- `increaseKey(e, amt)`
- `decreaseKey(e, amt)`
- `remove(e)`
- `newQueue union(q1, q2)`

## How can we represent this?
There are any number of ways we could implement such a structure, each with its own corresponding benefits and weaknesses.  
We're going to focus on utilizing heaps.
## Heap-ordered binary trees
### ^?
A heap-ordered binary tree is defined as a complete binary tree, with a single element per node, and is filled level by level, left to right. Since this is a binary-heap, any one node has a maximum of two children. Please note, such a heap does not obey the binary search tree property, rather, it obeys the heap property.
### Calculating the height
The height can be calculated at any time as `O(log(N))`, with N being the number of nodes.
### Heap property
Obeying the heap property requires that each node only has a single element, and each node's parent's key is less than its own key. In such a case, the root must always be the minimum element. We can create a tree with a different ordering property by changing the 'less than' to a 'greater than' or any extranneous ordering method. 
### Percolate Up
Percolate up is an operation whch is used for both decreaseKey and insert.  
`percolateUp()` continously swaps itself and its parent if its key is less than (or whatever ordering rule) than its parent. 
### Percolate Down
Percolate down is an operation whch is used for both increaseKey and deleteMin.  
`percolateDown()` continously swaps itself and its parent if its key is more than (or the inverse of whatever ordering rule) than its parent. 
### DecreaseKey
This function requires that you know where the element is, since there is no find.  
Just decrease the element's key, then call PercolateUp.
### IncreaseKey
Same thing as above, just increase the key and call PercolateDown.
### Insert
Add whatever element as a new leaf, then run percolateUp on the element.
### DeleteMin (or potentially max!)
The element you are looking to delete is always going to be the root of the tree! That is the value of using such a structure. To delete an element, swap it with a leaf (usually the last leaf), then call percolateDown on the new root.
### Binary Heap -> Array Representation
It is easy to look at some heap and visualize it as a tree, as we have nodes with children, but we can represent the whole structure in an array!  
Why? This is beneficial since when we want to insert a new leaf, we can just go to the last elemenet in the array, then call percolateUp. Similairly for delete, we just need to swap the first element with the last, then percolateDown on the root.  
We can use the rule that any node's parent is its own index/2, its left child is 2\*i, and its right is 2\*i+1.
## HeapSort
We can use such a DS to sort elements. Take your input, and insert every element into the heap - O(n\*log(n)), then pop them all. *Magic!*
## Build Heap in O(N)
Rather than constructing the tree in an arbitrary manner, start with a random array, start halfway through, and run to the root, running percolate down. This will build a heap in O(N)!

# d-Heaps and Leftist Heaps
## What is a D-Heap?
Binary heaps have two children, but there is a case to be made for more children. Having a wider node structure rather than a deep structure can help optimize different kinds of operations.
### Operations
 - insert ![equation](https://latex.codecogs.com/gif.latex?O\(log_d&space;n\))
 - deleteMin ![equation](https://latex.codecogs.com/gif.latex?O\(d&space;log_d&space;n\))

By using these two properties, we can optimize the tree for our particular use case.
## Leftist Heap
A leftist heap is a heap-ordered binary tree where the NPL(leftChild) >= NPL(rightChild) for every node.
### Why?
Sometimes we need to do more than just have two heaps, we need to merge them. Imagine a system running a job on two nodes, and for whatever reason one drains. Assuming it somehow has a failure script, the scheduled jobs and processes on the failed node now must to be merged onto the other machine. This problem of merging two heaps quickly s solved by leftist heaps.
### Null Path Length (NPL)
Null Path Length is defied as the shortest path between X and a null pointer.  
NPL(X) = length of right path from X.
### Operations
- Merge - Defined below
- Insert - Create a single node heap and marge the children.
- DeleteMin - Delete the root, and merge the children

All operations are O(log(N))
### Merge
Assume the root of H1 is <= root of H2. Recursively merge H2 with the right child of H1, and make the result the new right child of H1. Then swap the left and right children of H1 to keep the leftist property. 

# Search Trees
Search trees exist to help search over an ordered universe. Sometimes we need a certain amount of hierarchal data returned in an effecient manner.  
With a search tree, we have a set of nodes which can be reached by some sort of path. This path is made up of edges, and the number of edges it takes from A to B is the path length. The depth of a node is defined by the number of edges between it and the root.
## Traversal
Traversals allow us to visit all of the elements in a tree in some sort of order.
#### PreOrder Traversal
Preorder traversal:
1. Visit the root
2. Go to left subtree, and call preorder(leftSub)
3. Go to right subtree, and call preorder(rightSub)

#### PostOrder Traversal
Postorder traversal:
1. Go to left subtree, and call Postorder(leftSub)
2. Go to right subtree, and call Postorder(rightSub)
3. Visit the root

## Binary Search Trees
### Properties
Each node has at most two children. For any given node, the left children/subtree will always be less than the key, and the right children/subtree will always be greater than the key.
### Operations
(I'm not going to go through a few of these)
- Find()
- Insert()
- Delete()
- FindMin()
- FindMax()

### How does insert(e) work?
First ru find and see if the node exists, if not, insert X at the last spot seen on the path.
### How does delete(e) work?
Delete gets messy.
#### e is a leaf
If it is a leaf, then just delete it.
#### e has one child
If it has a single child, then just get delete the node and relink the child to the parent.
#### e has two children
Replace it with the smallest node in the right subtree of X, and delete said node.  
or: the largest node in the left subtree, and delete said node. 
### Other details
In the worst case, a BST can have a height equal to a linked list.  
The internal path length is usually O(nlogn) as well.
# Balanced Search Trees
## Why?
Sometimes we actually need a decent tree. Having a balanced tree is fundementally important to accessing elements in a consistent manner.
## AVL Trees
Gaurenteed O(logN) worst case for insert/delete operations.
### How? (AVL rules)
AVL Trees require that the heights of its children can differ by at most 1.
### Height properties
- An empty subtree has a height of -1.
- The height of a tree is 1+max(height(left), height(right))
- The height is consistently O(logN)
- The height is bounded by ![equation](https://latex.codecogs.com/gif.latex?1.44*log{n&plus;2})

### Tree Rotations
Tree rotations structurally change the tree on access operations.
#### Why?
By implementing these simple rotations for insert, delete, and search, we can enforce the AVL properties by consistently restructuring affected portions of the tree.
#### Rebalancing overview
An imbalance occurs either due to:
1. Insertion into the left subtree of the left child of a node that needs rebalancing, or the right subtree of the right child.
2. Insertion into the left subtree of the right child of a node that needs rebalancing, or the right subtree of the left child.

1 is fixed with a single rotation, and 2 with a double rotation.
#### Single Rotations
![single rotation diagram](https://upload.wikimedia.org/wikipedia/commons/2/23/Tree_rotation.png)
#### Double Rotations
![double rotation diagram](http://pages.cs.wisc.edu/~siff/CS367/Notes/AVLs/double-after.gif)
### Removal
Find the element, delete it, adjust tree height, rotate. 
### Complexity Bounds
Everything is O(logN)!
# Splay Trees
## Why?
AVL is hard, we don't want to have to do a bunch of confusing work for our tree to work.
## Splaying
Rather than have some confusing rules for the tree, lets just 'splay' the tree on every access. Essentially just keep splaying at some sort of a node until said node becomes root! This method is O(logN), and will ensure that the tree stays balanced! To splay, there a few different types of roations that must be considered.  
Splying also has the side benefit of roughly halving the depth of all nodes along the access path.
### Zig
This case is valid when the parent of a node is the root. Just apply the single rotation we mentioned earlier:
![zig rotation diagram](https://upload.wikimedia.org/wikipedia/commons/thumb/2/2c/Splay_tree_zig.svg/1418px-Splay_tree_zig.svg.png)
### Zig-Zig
This is the case if the parent of a node is not the root and the node and the parent of the node are both left or both right children:
![zig-zig rotation diagram](https://upload.wikimedia.org/wikipedia/commons/f/fd/Zigzig.gif)
### Zig-Zag
This is the case if the parent of a node is not the root and the node and the parent of the node are alternating children:
![zig-zag rotation diagram](https://upload.wikimedia.org/wikipedia/commons/6/6f/Zigzag.gif)
## Access
Access returns a pointer to the item it is searching for, and if it is unavailable it returns a null pointer. We search from the root fown, and if we find it, splay at the node. If we reach a null node, then splay at the last accessed node.
## Join
Join combines two trees into a tree and returns the resulting tree, assuming that all elements in the first tree are smaller than the second. First access the largest item in the first tree, then make the second tree the root's right child.
## Split
Split returns two trees, one of which has all of the elements less than or equal to the requested element, and a second of which has all of the items which are greater than it. First do access for the element, if the root > x, break the left child, otherwise break the right child.
## Insert
Insert the element into the tree by performing split, then making a new tree with the element as the root and subtrees from the split.
## Delete
Access the element, delete root, join the two remaining subtrees.
## Complexity
Any m operations takes O(m log N)
# Amortized Analysis
## Why?
Sometimes one or two operations can b expensive, but super cheap down the line.
If the total cost of N operations is T(N), then the amortized cost of each of those N operations is T(N)/N
## Aggregate Method
Basically just consider the number of operations that occur for a cycle, add them up intelligently, and check what your true per operation cost it.
## Accounting Method
Assign charges to operations, some more or less than the true cost. The data structure acrues credit, which can pay for amoritized cost down the line. Choose costs carefully so that the credit of such operations is never negative.
## Potential Method
Imaging potential energy in physics, and essentially as operations occur they can increase or decrease the potential energy of the structure. This relies on the intelligent defining of some sort of consistent state-based potential function to utilize. The potential of a DS ust be measured in a consistent manner.
# Graphs
## What's a graph?
A graph is a way of having a ton of distributed data points to each other and demonstrate correlations between data points.
Imagine a traffic diagram between cities, the cities would be the vertices, and roads would be the edges. Or we can imagine some hell of a node projects with hundreds of modules, all requiring some sort of version dependency between themselves. Or Facebook mapping friend networks, or LinkedIn showing how far a potential connection is from your circle.
### Vertices
A vertice is another name for a node, and holds some sort of data.
### Edges
An edge is a connection between two vertices. Edges can have weight and direction. Weight represents the path cost, and direction is literal.
### Directed vs Undirected
A directed graph has edges which have a fixed direction of travel. An undirected graph is a graph where you can go back and forth on any given edge. Any undirected graph can be represented as a directed graph, but with twice the number of edges.
## Representations of graphs
There are two common ways to represent a graph.
1. An adjacency matrix, also known as hell on earth, requires O(V^2) space to hold a graph. Each directed edge s shown as an 'x' on two vertices row and column in a matrix. For any number of vertices greater than 5 this is ridiculous and ineffecient.
2. An adjacency list liss all valid vertices, and the following edges between them. This is significantly more effecient, and only takes O(|E|) space.

## Paths
A path is a route taken along edges between 2 vertices. You can of course have a path between n vertices, but what matters is the last two and the corresponding edges you took to get there. Such edges have a corresponding weight, and one can caluclate a path weight from this.  
Paths can also be cyclic if they have the same first and last vertice.
## Minimally Connect Graph = Tree
A minimally connected graph is a graph without cycles. It can also be represented as a tree. We can also name some random node as a root to more easily represent such a graph.
## ST Connectivity
This is a common question asking given some node s and another t, is there a path between the two?
## Connected Components
A simalair question: Given a node, what are all of the reachable nodes? The set of elements that follows contains all connected components.
## Breadth First Search (BFS)
We essentially start at a node, then explore, and keep track of where we have visited. Each node that we visit will get a level number, which is defined as how far a given node is from the start node s. Any neighbr of s, for example, would be on level 1. Exploring in this fashion will result in a BFS tree. We know there is a path between s and t if t shows up in the BFS tree.  
O(|V|+|E|)
## Depth First Search (DFS)
Starting at s, take the first edge and continue recursively until we hit a dead end. Backtrack until we get to a node with an explored neigbor, explore. This method goes deep, then backtracks as necessary. As one progresses through the graph, we keep track of nodes we have visited and add such nodes to a DFS tree. If we have already seen said element, then we mark them in the DFS tree as having a back-edge between the two nodes. This represents some sort of bi-cnnectivity.  
O(|V|+|E|)  
Fun facts:
1. "For a recursive call DFS(u), all nodes that are marked *explored* between the invocation and the end of the recursive call are descendants of u in T."
2. "Let T be a DFS tree, let x, y be two nodes in T that have an edge between them in G, but (x, y) is not an edge of T. Then, one of x or y is an ancestor of the other."2

## BiPartititeness
A graph is bipartite if it can be partitioned into two categories and perfectly two-colored.
![bi-partite example image](http://www.csie.ntnu.edu.tw/~u91029/BipartiteGraph1.png)
Turns out a graph G is bipartite if and only if it does not contain an odd-length cycle.
### N-Colorable
Same idea, but now instead of 2 colors, what about N colors?
## Bi-Connectivity
A graph is bi-connected i we must delete at least two nodes to get rid of a given node.
### Why?
This is important if we are trying to keep safe references to some data, or ensure that it is easil accesible in a multitude of fashions. Or if we are a mapping application searching for alternate routes to a destination due to a route closure.
### Articulation Point
An articultation point is a single node where we can remove said node and split a graph.
### How to check
You can check for Bi-Connectivity and find articulation points by applying the Hopcroft-Tarjan algo: Run a DFS while keeping track of the position of each order in the DFS tree, and the lowesy number reachable vertex from every vertex. Low is defined by min(Num(v),{Num(W) : (u,w) being a backedge for a descendant u of v}). We can caulculate all low values in linear time.
Any given node is an articulation point if
1. The root is an articulation point if it has more than one child
2. Any non-root node v is an articulation point if it has a child w where the low(w) >= num(v).

## Topological Sort
Let's say we want an ordering in which you have a directed acyclig graph (dag) and you need to find an ordering for all nodes to be done such that all dependencies are respected. For every edge you want the nodes to be perfectly in order, and to point from smaller nodes to larger nodes.
### Why?
This matter for dependency generation and other mapping applications. Easy to come up with examples, just think about it.
### Forming a topological ordering
1. Compute all vertices incoming edges, queue all those with zero.
2. Pick a vertex from the queue, schedule it.
3. For each adjacent vertex, decrement its incomind edges and add each adjacent vertex to the quesue if it has 0 incoming edges.
O(n+m)

## Strong Bi-Connectivity
If we have a path from u to v and from v to u. This matter for directed graphs as we may not always have a path back.  
How do we check this?
1. Perform a DFS
2. Number the vertices in post-order, as their recursive calls finish
3. Construct the reverse graph, flip all edge directions
4. Perform a second DFS from the highest number vertex, output each subtree, and remove it from the graph.

# Applications of DFS
# Union Find Data Structure
## Background
Lets say you have a bunch of disjoint sets. Each element is contained in a single set.
### A set of sets
This data structure is essentially a massive set of sets, where elements shift between sets to help optimize their retreival.
## Basic Operations
With the union find stucture we focus on two operations
- `setName find(element)`
- `union(set1, set2)`

## Quick Find
Imagine some sort of an array for N elements, of size N. Find is just lookup element I, so O(1), but union requires access and checking, so O(N).
## Quick Union
Each set is a tree, and you find elements by following parent pointers to the root. Finding is hard in this case, O(N), but union is imeediate since we're just moving pointers around, O(1).
## Smart Union
Now let's have the union just make smaller trees point to the bigger tree's root. This keeps the tree's height relatively short.
### Why does this work?
This works since the when union is performed, the depth only increases if its root becomes a new child. If the depth increases, then its new tree size must be > 2\*oldTreeSize. This means that find is now O(logN), and union is O(1).
## Path Compression
While performing find, take all pointers on the access path to the root, and just repoint the pointers to the root.
## Inverse Ackermann
One find can still be O(logn), but future finds now run in O(\invackerman(f,u)) which is essentially constant time.

# Mininum Spanning trees
## Why?
Sometimes we want to know what the smalles possible tree is between some nodes.
## Cut Theorem & Greedy Algorithms
For any given cut, the lowest weight edge crossing the cut must be in the minimum spanning tree. If there is a tie, each one is in *a* minimum spanning tree.
## Prim's Algorithm
Keep adding the cheapest edge joining a node to another vertex.
## Kruskal's Algorithm
Given some start vertice, just add cheapest edges, and make sure there are no cycles. Keep adding cheapest edges until there are no unreachable nodes or we run out of edges.

# Shortest Path
## Structural Properties
- Prefixes of shortest paths are shortest paths
- A shortest path does not always exist
- A shortest path tree does always exist

## Djkstra
### Some quotations of his on lecture slides which are fun
- "The use of COBOL cripples the mind; its teaching should, therefore, be regarded as a criminal offense."
- "It is practically impossible to teach good programming to students that have had a prior exposure to BASIC: as potential programmers they are mentally mutilated beyond hope of regeneration."
- "About the use of language: it is impossible to sharpen a pencil with a blunt axe. It is equally vain to try to do it with ten blunt axes instead."
- "Object-oriented programming is an exceptionally bad idea which could only have originated in California."

### Algorithm
Given arbitary non-negative edge weights.
## Acylcic Graphs
## Bellman Ford
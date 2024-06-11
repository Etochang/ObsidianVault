Definitions:
- Graph: G = (V, E) consists of:
	- A set of vertices/nodes V, and a set of edges E, where each edge has two end vertices
- Edge Type:
	- Directed: Ordered pair of vertices represented as (u, v) from u to v
	- Undirected: Unordered pair of vertices represented as {u, v}
	- Loop: edge whose endpoints are equal
	- Multi-edge: Two or more edges joining the same pair of vertices
- Graph Type:
	- Undirected: consists of V, a nonempty set of vertices, and E, a set of unordered pairs of distinct elements of V
	- Directed: G(V, E), set of vertices V and set of Edges E that are ordered pairs of elements of V
	- Complete: is a graph that contains exactly one edge between each pair of distinct vertices, aka all nodes are connected to each other via an edge
- Degree:
	- Undirected: number of edges connected to a vertex
	- Directed: deg- = number of edges that go into vertex. deg+ = number of edges that go out
- Cycle: if a loop can be made in a graph, cyclic, else acyclic
- Subgraph: H(V', E') where everything is subset
- If graph is weighted, adjacency matrix uses NULL instead of 0 to represent no connection.
#### BFS, DFS - Characteristics
DFS:
1. Head all the way down, Hits a dead end, Backtracks until unexplored direction is found
2. Repeat 1 until backtrack to start with all explored or find what you want
- If a node's timestamps are both null, then undiscovered; If a node's discover time is not NULL, then visited/discovered; if a node's finish time is null, then it's unexplored.; if a node's timestamps are both not NULL, then it is explored.
- if a.d < b.d, then a is a predecessor of b, and b is a descendant of a.
- Implement with a stack that stores Node struct objects
BFS:
1. Check the root node, Check all nodes that are 1 edge away from the root, Check all nodes that are 2 edges away from the root
2. Enqueue all adjacent nodes once current node is visited
- Uses FIFO queue with Node struct objects
#### Topological Sort of DAGs

- Only applies to **Directed Acyclic Graphs**
	- If graph is undirected or cyclic, there is at least one node that is both an indirect/direct successor and predecessor to a node, which screws up the topological order.
- Insert from right to left least finish time to greatest finish time
#### MST with Prim's and Kruskal's

- Spanning tree: subgraph of G(V, E) that spans the graph (includes all vertices), **V vertices, V-1 edges**
- Minimum Spanning Tree
	- Applicable to Weighted Undirected Graphs; An MST is an acyclic subgraph of G such that total edge weight is the smallest possible and all it is a spanning tree of G.
- Prim's
	- Pick a random node as the starting point of the Tree
	- From all nodes not in Tree, pick the node whose distance to any node in Tree is the smallest, and add that edge in to Tree, where a candidate edge must have one end in Tree, and the other not in Tree.
	- Keep repeating 2 until all nodes are in Tree; Space complexity = O(V+E)
- Kruskal's
	- Sort all edges in ascending order
	- From the smallest edge, if this edge does not create a cycle with the ones in the Selected Subgraph, then add this edge into Selected
	- until all nodes are connected by the edges in Selected; Space complexity = O(E)

#### Single-Source Shortest Path w/ Dijkstra's

1. Set source distance to 0, all others to infinity
2. select smallest distance to source value, then relax the neighbors of this smallest distance node. mark as visited, then repeat this process until all nodes are selected; Space complexity of O(V)

#### Greedy Algorithm

- A greedy algorithm always makes the best choice at that moment, but doesn't always result in the optimal solution.

#### Basic Philosophy of Optimal Substructures for DP

- start with the small: Set up the base/easy cases first; Make the saves: Put away the intermediate results in some extra places; Reuse the saves for the big.

Where applicable: Overlapping subproblems; Optimal substructures

#### Minimum Coins for Change using 1D array

- 1D array - O(N) time and space complexity, N is total amount to fill up; Fill in base cases first, then do it according to algorithm

#### Length of the LCS using 2D array

Maintain and populate a 2D array table c where c(i, j) = length of an LCS of prefixes Xi and Yj; c(0, any) and c(any, 0) are all 0's; target is c(m, n), where m is the length of the sequence X and n is the length of the sequence Y.
- If elements xi = yj, then c(i, j) =  (i-1, j-1) + 1; if not, then pass on the max of the previous top or left.
- remember c(i, j) is the length of an LCS of Xi and Yj
- At row i in c(,) we are essentialy comparing Xi vs. Y1, 2, 3...n

#### Minimum Scalar Multiplications for Chained Matrix Product using a 2D array

- When multiplying mxn and nxq matrix, usually need mxnxq scalar multiplications.
- m(i, j) = number of minimal scalar multiplications for Ai Ai+1 ... Aj
- m(1...n, 1...n) for all number of scalar multiplications needed to obtain chain product A1 ... An. If Ai ... Aj is computed between intermediate chain products (Ai ... Ak)(Ak+1 ... Aj):
	- Number of scalar multiplication to get Ai ... Ak is m(i, k)
	- Number of scalar multiplication to get Ak+1 ...  Aj is m(k+1, j)
- A1, A2, A3 ... An = p0 x p1, p1 x p2, p2 x p3 ... pn-1 x pn
- The number of scalar multiplication to multiply intermediate chain products Ai ... Ak and Ak+1 ... An is pi-1 x pk x pj.
- Diagonal is 0, rest is min(m(i, k)+m(k+1, j) + pi-1 x pk x pj) for k = i, i+1, ..., j; O(n^3) time complexity

**Fewest than all the others = fewer than others = same means false**

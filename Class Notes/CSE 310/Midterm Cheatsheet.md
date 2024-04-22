- **LOWER BOUND FUNCTION HAS TO BE EQUAL TO THE UPPER BOUND FUNCTION FOR TIGHT BOUND TO EXIST**. **DITCH ALL CONSTANT MULTIPLIERS**, keep unique terms.
- if $f(n) \in O(s(n))$ and $g(n) \in O(r(n))$,
	- $\forall{c > 0}(c\cdot f(n) \in O(s(n)))$; $f(n) + c \in O(s(n))$; $f(n) + g(n) \in O(s(n) + r(n))$; $f(n) \cdot g(n) \in O(s(n) \cdot r(n))$


| Time Complexity Notation | Comparison Symbol | Limit |
| ---- | ---- | ---- |
| $f \in O(g)$ | $f \le g$ | $\lim_{x \rightarrow \infty} \frac{f(x)}{g(x)} < \infty$ |
| $f \in \Theta(g)$ | $f = g$ | $\lim_{x \rightarrow \infty} \frac{f(x)}{g(x)} \in \mathcal{R^+}$ |
| $f \in \Omega(g)$ | $f \ge g$ | $\lim_{x \rightarrow \infty} \frac{f(x)}{g(x)} > 0$ |

- MergeSort: $T(n) = T(n/2) + n$, $\Theta(n \log{n})$. Out-of-place: In-place: doesn't need extra space, Out-of-place: vice versa. QuickSort: Worst case: $O(n^2)$, Best case: $O(n \log n)$; Called Quick b/c Conquer and Combine step is done together.

- Root is at `A[1]`, Parent of node `A[i]` is at `A[floor(i/2)]`, Left child is at `A[i*2]` and right at `A[i*2+1]`. Capacity of heap is sizeofarray - 1; size of heap is number of nodes. Heaps are **Complete Binary Trees**, Max: $\ge$, Min: $\le$.
- Max-Heapify - Only applicable when **Both subtrees are valid max heaps**. If parent value less than any child value, swaps parent value with greatest child value. Then checks to see if max heap property is retained on the now-switched parent value. $O(\log n)$ because worst case scenario is swapping $\lfloor \log_2 n \rfloor$ levels.  
- BuildHeap - Maxheapify starting from first node with NON-NULL children, ending at root.  $T(n) = \sum_0^{\lfloor \log n \rfloor} (\lceil \frac{n}{2^{h+1}} \rceil \cdot O(h))=O(n)$  
- HeapSort - Swap root with last element/position, then 'pop' it out of the heap. Heapify the new root node, and repeat. $O(n \log n)$. 

$T(n)$ is the worst case runtime on a n-size input, and consists of three parts: \# of subproblems (a), How much input each subproblem takes care of, (1/b) Cost of non-recurrent operations (n^d). if n = 1, T(n) is constant. Can only use master theorem if constant number of subproblems, equally sized sub-input, non-recursive ops can be expressed as O(n^d).
##### Quick Select (kth smallest)

(1) Take element as pivot (2) run full $\Theta(n)$  scan to create left (<pivot) and right (>pivot) partitions, swap pivot into middle (3) if the pivotindex is k-1, return, else if pivotindex is greater, QuickSelect kth in L, else QuickSelect (k-1-pivotindex )th in R. $O(n^2)$ at worst, $\Theta(n \log n)$ on average

##### Median of Medians (MoM) kth smallest

**Find-Pivot:** (1) Divide n-sized A[] into subgroups of 5 elements (2) sort all subgroups ($O(1)$) (3) Put all $\lceil \frac{n}{5} \rceil$ medians into new input array (4) repeat recursively until only one subgroup of $\le$ 5 elements. Median = MoM pivot. -$T(n/5)$-

**Partition-and-select:** (1) partition around the pivot -($O(n)$)- s.t. left is $\le$ and right is $\ge$ (2) if median of group is $\le$ MoM pivot, then $\frac{3}{5}$ of the group is $\le$ MoM pivot. $\frac{1}{2} \lceil \frac{n}{5} \rceil$ groups of 5 means $\frac{3}{2} \lceil \frac{n}{5} \rceil = \frac{3}{10} n$ elements $\le$ MoM pivot, and $\frac{7}{10} n$ elements who are unknown. Recursively select, either left or right, like Quick Select  -($T(7/10\cdot n)$ worst case scenario)- If adding the $T$ parts and is $\ge$ $n$, then $O(n \log n)$ instead of $O(n)$. Substitute T(n) and other T terms with cn to prove that T(n) $\le$ cn.

#### BST
- Not complete binary tree, but has property left-child subtree values $\le$ parent $\le$ right-child subtree values. Single node is legit too. If every node is missing a subtree, worst case, minimal height of $\lfloor \log_2 n \rfloor$ is best. Search time is  respectively $O(n)$ and $O(\log n)$. 
- $O(n)$ to insert one key, $O(n^2)$ to insert $n$ keys in worst case.
- Removing - Case 1: Removing a leaf node, nothing needs to be done - Case 2: Node only has one subtree - attach severed subtree to removed node's location - Case 3: Node has both children - find closest key (left-most of right subtree (in-order successor) or right-most of left), copy content to current node, delete the key afterwards
- in-order: left-root-right | pre-order: root-left-right | post-order: left-right-root
##### 2-3-4 Tree

- All leaf nodes are on the same level, nodes can now be up to 4-way-splits. Search: one key is same as BST, $>$ 1 key check different "splits". $O(\log n)$
- Insertion: maintains depth condition, fill up leaves whenever possible. Add elements only to existing nodes. except for empty root. At most $O(\log n)$, regardless of split and cascade. Max travel distance of key is 2h - 1, where h is height, down to leaf and past old root. 
- Split ($O(1)$): when inserting into 4-way node, split now-5-way into two nodes on the same height, 2-1 split and 3rd gets LIFTED UP to the parent node, creating a new root if necessary. **ONLY WAY 2-3-4 TREE CAN GROW IN HEIGHT**. Cascade happens when split causes split in parent.
- Deletion: 3-way and 4-way nodes are just fine. Transfer - 2-way, sibling not 2-way: pull one from parent, replace parent with one from sibling. Fuse - 2-way, sibling 2-way: pull one from parent, then fuse with sibling to make 3-way node. Cascade when parent is left empty by this. $O(\log n)$ 

##### Red Black Tree

- BST, edges either red or black. **On any from-root-to-null-leaf path, we have 3 hard laws/violations:**
	- No consecutive two red edges; Same number of black edges, excluding edges connecting null leaves; Edges connecting the null leaves are always black. 
- Red edge == internal order inside 3- or 4-way node, black edge == connecting 2-3-4 tree nodes. - - O == [b]O[b]; - - - O == [b]O r [b]O[b] *or* [b]O[b] r O[b]; - - - - O ==  [b]O[b] r O r [b]O[b]. Height is between $\log_4 n$ and $\log_2 n$, so search always takes $O(\log n)$. 
- Insertion - Find a leaf and re-color the coming edge:
	- (1) Perform search to find the leaf where the key should be added (2) replace the leaf with an internal node with the new key (3) color the incoming edge of the new node red (4) add two new NULL leaves, and color their incoming edges black (5) **handle any violation**. () = subtree, [] = null

| Case                                                                                                                                        | Former Tree Structure                                                                | After Violation Handling                                                                                                              |
| ------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------- |
| Incoming edge of P is black, like inserting into 2-way node of 2-3-4                                                                        | [b]$\hat{N}$[b] r $P$(b) b $\bar{G}$(b)                                              | [b]$\hat{N}$[b] r $P$(b) b $\bar{G}$(b)                                                                                               |
| Incoming edge of P is red, like inserting into 3-way node and new key is larger/smaller than both existing keys                             | [b]$\hat{N}$[b] r $P$(b) r $\bar{G}$(b) \|\| (b)$\bar{G}$ r (b)$P$ r [b]$\hat{N}$[b] | right or left rotation respectively: [b]$\hat{N}$[b] r $\bar{P}$ r (b)$\hat{G}$(b) \|\| (b)$\hat{G}$(b) r $\bar{P}$ r [b]$\hat{N}$[b] |
| Incoming edge of P is red, like inserting into 3-way node and new key is between both existing keys                                         | (b)$P$ r[b]$\hat{N}$[b] r $\bar{G}$(b) \|\| (b)$\bar{G}$ r [b]$\hat{N}$[b]r$P$(b)    | (1) rotation of N and P s.t. G will be next to N (2) left/right rotation like last case                                               |
| Incoming edge of P is red and sibling edge of G-P is red as well, like inserting one into a 4-way node and performing the split and cascade | [b]$\hat{N}$[b] r $P$(b) r $\bar{G}$(r) \|\| (b)$P$ r[b]$\hat{N}$[b] r $\bar{G}$(r)  | Color edge G-P and its sibling edge black, and color the incoming edge of G red; **Check the violation upward regarding G**.          |

- $O(\log n)$ in both insertion and violation handling.
- Deletion ($O(\log n)$): Could swap with in-order predecessor or successor, then delete the node while coloring incoming edge black.
	- Double Black Edge: $v$ is the swapped leaf node to remove, $u$ is a null node. If the incoming edge of $v$ was red, color new incoming edge of $u$ black, and if $v$ was black, color it double black | Deleting a node with a red incoming edge is effectively removing one from a 3- or 4-node.

| Case                                                                                                                                                                                                                                                    | After Violation Handling             | 2-3-4 picture                        |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------ | ------------------------------------ |
| If double black's sibling edge is black and one of its children edge is red, like transfer only. Double black edge is technically two black edges connected via null node.                                                                              | ![[Pasted image 20240326132833.png]] | ![[Pasted image 20240326132902.png]] |
| If double black's sibling edge and its children edges are all black, color the sibling edge red, and if double black's parent's incoming edge is (a) red, color it black (fuse) (b) black, color it double black then check upwards (fuse and cascade). | ![[Pasted image 20240326133052.png]] | ![[Pasted image 20240326133202.png]] |
| Do the readjustment without removing the double black if double black's sibling edge is red.                                                                                                                                                            | ![[Pasted image 20240326134029.png]] |                                      |
#### The Complexity Notations - Big-O, Big-Omega, Big-Theta

- The Worst Case - **The Upper Bound** of running time. Time Complexity means this by default. Big-O is used denote the asymptotic upper bound. Definition: For a given $g(n)$, $O(g(n))$ is the set of functions $\{f(n): \exists (c, n_0 \ge 0) \forall (n \ge n_0) ,(0 \le f(n) \le c \cdot g(n)\}$. So if $f(n)$ is Big-O of $g(n)$, it means that g(n) is the upper bound of growth for f(n), or that f(n) is a member of the set O(g(n)). For Polynomials - Look at highest term, or "pull-up to g(n) level" proof.
- The Best Case - **The Lower Bound** of running time. Big-$\Omega$ is used denote the asymptotic lower bound. Definition: For a given $g(n)$, $\Omega(g(n))$ is the set of functions $\{f(n): \exists (c, n_0 \ge 0) \forall (n \ge n_0) ,(c \cdot g(n) \le f(n) \le \infty) \}$. So if $f(n)$ is Big-$\Omega$ of $g(n)$, it means that g(n) is the lower bound of growth for f(n), or that f(n) is a member of the set $\Omega$(g(n)). For Polynomials - Look at highest term, or "pull-down to 0 level if not highest term" proof.
- Tight Bound - Big-$\Theta$ is used denote the asymptotic **tight** bound. Definition: For a given $g(n)$, $\Theta(g(n))$ is the set of functions $\{f(n): \exists (c_1, c_2, n_0 \ge 0) \forall (n \ge n_0) ,(c_1 \cdot g(n) \le f(n) \le c_2 \cdot g(n)) \}$. So if $f(n)$ is Big-$\Theta$ of $g(n)$, it means that g(n) is the **tight** bound of growth for f(n), or that f(n) is a member of the set $\Theta$(g(n)). For Polynomials - Look at the highest term, or find a g(n) such that Big-O and Big-$\Omega$ both work. **LOWER BOUND FUNCTION HAS TO BE EQUAL TO THE UPPER BOUND FUNCTION FOR TIGHT BOUND TO EXIST**.
- **DITCH ALL CONSTANT MULTIPLIERS**, keep unique terms.
- if $f(n) \in O(s(n))$ and $g(n) \in O(r(n))$,
	- $\forall{c > 0}(c\cdot f(n) \in O(s(n)))$; $f(n) + c \in O(s(n))$; $f(n) + g(n) \in O(s(n) + r(n))$; $f(n) \cdot g(n) \in O(s(n) \cdot r(n))$


| Time Complexity Notation | Comparison Symbol | Limit |
| ---- | ---- | ---- |
| $f \in O(g)$ | $f \le g$ | $\lim_{x \rightarrow \infty} \frac{f(x)}{g(x)} < \infty$ |
| $f \in \Theta(g)$ | $f = g$ | $\lim_{x \rightarrow \infty} \frac{f(x)}{g(x)} \in \mathcal{R^+}$ |
| $f \in \Omega(g)$ | $f \ge g$ | $\lim_{x \rightarrow \infty} \frac{f(x)}{g(x)} > 0$ |


#### Divide and Conquer - MergeSort, QuickSort

1. Divide the problem into smaller sub-problems; Conquer the sub-problems by solving them *recursively*, or solve trivial subproblems w/o recursion (extreme cases); Combine the solutions to the sub-problems

Incremental InsertionSort: From index 0 to index size-1, swap value incrementally back until value meets one that is less than it (or at 0).

- MergeSort: Divide n-element sequence into two equal halves, call MergeSort recursively on the two unsorted halves, merge the two **already sorted** halves into a sorted sequence of n-elements. Extreme case: if n is 1, then return as is b/c a 1-element sequence is already sorted. $T(n) = T(n/2) + n$, $\Theta(n \log{n})$. Out-of-place: In-place: doesn't need extra space, Out-of-place: vice versa.

- QuickSort for ascending order: Pick a **pivot** element (usually last element), Scan the sequency one by one, if smaller than pivot, throw to left-partition, otherwise throw to right-partition, call quicksort recursively on left-partition and right-partition, concatenated {sorted left, pivot, sorted right} is the sorted sequence. Extreme case: if n is 1, then return as is. Worst case: $O(n^2)$, Best case: $O(n \log n)$; Called Quick b/c Conquer and Combine step is done together.

#### Recurrence Analysis $T(n)$ of Divide and Conquer and the Master Theorem

$T(n)$ is the worst case runtime on a n-size input, and consists of three parts: \# of subproblems (a), How much input each subproblem takes care of, (1/b) Cost of non-recurrent operations (n^d). if n = 1, T(n) is constant. Can only use master theorem if constant number of subproblems, equally sized sub-input, non-recursive ops can be expressed as O(n^d).
$$T(n) = aT(n/b)+O(n^d)$$
#### Heap - Max Heapify, BuildHeap, HeapSort, Priority Queues

- 0 index slot is never used when representing a tree. Composed of **NODES** as slots, can be NULL, non-empty tree has a **ROOT** node. Each node connects to **PARENT** node, **LEFT CHILD** node, and **RIGHT CHILD** node. Accordingly, left and right subtree. Distance of each node to the root defines the layer the node is at. If both children are NULL, then the node is a **LEAF**. Root is at `A[1]`, Parent of node `A[i]` is at `A[floor(i/2)]`, Left child is at `A[i*2]` and right at `A[i*2+1]`. Capacity of heap is sizeofarray - 1; size of heap is number of nodes. 
- Heaps are **Complete Binary Trees**, all layers except the last are full and last layer is filled from left to right. In a **MAX HEAP**: any parent node value is always $\ge$ NON-NULL child node values. **MIN HEAP**: any parent node value is always $\le$ NON-NULL child node values. 
- Max-Heapify - Input: heap tree, whose root node is `A[i]` - Only applicable when **Both subtrees are valid max heaps**. NULL node is considered a valid max heap. If parent value less than any child value, swaps parent value with greatest child value. Then checks to see if max heap property is retained on the now-switched parent value. The "Sinking" procedure. $O(\log n)$ because worst case scenario is swapping $\lfloor \log_2 n \rfloor$ levels.  
- BuildHeap - Given a random array, convert it to a proper heap array. Start with the leaf nodes, bottom-up, do max heap starting from first node with NON-NULL children, ending at root. Once max heap goes past, the node is considered the root of a max heap. $T(n) = \sum_0^{\lfloor \log n \rfloor} (\lceil \frac{n}{2^{h+1}} \rceil \cdot O(h))=O(n)$  
- HeapSort - Straightforward, first BuildHeap(A), then convert the heap array A to a sorted array. Since root of max heap is always the globally maximum, swap root with last element/position, then 'pop' it out of the heap. Heapify the new root node, and repeat. This way, the first biggest will be the last, the second biggest will be the second last, so on and so forth. $O(n \log n)$. 

#### Hash Table - Hashing and Collision Resolving Techniques

- Phone Book = Hash Table, Index Page/TOC = Hash Function, Name = Key, Phone Number = Value. Hash Table `d` equipped with hash function `hash()`, input key `k`, `hash(k)` yield address `i`, `d[hash(k)]` is the value (or the list where the value can be located). Each slot contains a pointer to a key-value pair/linked-list of key-value pairs.
- Hash function: Input - a key value, can be anything; Output - a \# that points to a slot in the Hash Table, all outcomes belong to a finite set with size equal to \# of slots. Output of hash function is **hash value**, applying function to key is called **hashing**. Example: taking mod of size. Good hash function approximately satisfies, "**an arbitrary key is equally likely to be hashed to any of the m slots of the hash table." 
- If `h(key1) == h(key2)`, this is a collision. Can either allow collisions or not. **Chaining** hash table just makes each slot a list, adding the new value to the head of the old values if a collision occurs, may waste slots. **Open Addressing** resolves collisions, and each slot stores *exactly one key,* but may fail to fit stuff in and be harder to locate values based on key.
	- Resolving Collisions over OA: we can update the hash value until an available slot is reached, if not reached, ditch the key and move on to the next key. **Linear Probing**: add an incrementing \# after the hash output if a collision happens, loop to 0 and go back to value if overreach. **Quadratic Probing:** additive is now a quadratic function of i, i is set to 0 after collision is resolved. i goes until n-1, where n is \# of slots. **Without Probing**: just ditch the key causing the collision. 
- Load Factor: ratio between \# of keys inside hash table and total \# of slots. Gives estimate of average search time.
202402061510
Meta Tags: #homework 
Tags: [[CSE 310]] [[heap]]

# Homework 3

- highest priority value at the root of the heap
- increase certain priority value inside the max heap while maintaining the max heap property.

Given a max heap array A (of size n), `Heap-Increase(A, i, k)` increases `A[i]` by `k`.

## PART 1A

Assuming that the root is at `A[1]`.

```
Heap-Increase(A, i, k) {
	//k > 0, adding k to A[i] 
	A[i] = A[i] + k;
	
	//Since A was already a max heap array, no need to check A[i]'s children for violations.
	//However, A[i] might have become bigger than its parent due to its increase. Swap the two if A[i] is bigger, if not, the array is still a valid max heap.
	int curr_i = i;
	if (A[floor(i/2)] < A[i])  {
		swap(A[i],A[floor(i/2)]);
		curr_i = floor(i/2);
	} else {
		//max heap property has been retained
		return;
	}

	//Now that the values are swapped, we again don't need to check the children at the new position of A[i], or A[curr_i]. This is because the former parent of A[curr_i] was already larger than A[curr_i]'s sibling in the first place, and A[curr_i] is greater than its parent. 
	// We just need to check if A[curr_i] is bigger than it's new parent. Now we can see a pattern: check if it is greater than its parent, if so swap, if not stop, and if the A[curr_i] node becomes the root, stop.
	//I will write the associated loop down below; I could consolidate the preceding lines into this, but I will keep them to show my line of reasoning.

	//while current node isn't root
	while (curr_i > 1) {
		//if parent is less than current node swap, else return
		if (A[floor(curr_i/2)] < A[curr_i])  {
			swap(A[curr_i],A[floor(curr_i/2)]);
			curr_i = floor(curr_i/2);
		} else {
			//max heap property has been retained
			return;
		}
	}
}
```

## PART 1B

The end case of `Heap-Increase` is when our node swaps to the root, or `curr_i = 1`. 

Let's give each group of comparison + swapping statements a constant time value of $c$, which we can factor out of our Big-O reasoning.

The worst case scenario is if our max heap's last level has only one leaf, and our increase of priority of that leaf makes it go to the root of the heap. This is because it has to travel the greatest distance in proportion to the \# of nodes.

So, with $L$ levels and one leaf, we have $n=(2^{L-1}-1)+1 = 2^{L-1}$ nodes, and we have to travel up the heap $L-1$ times. It is easy to see that
$$T(n) = \log_2n$$
for our `Heap-Increase` routine based off of these facts. The tightest bound for the routine is subsequently $O(\log n)$ - it can't be $O(1)$ since $T(n)$ depends on $n$. 


---
# *References*
[HW3 Spring 2024 - Google Docs](https://docs.google.com/document/d/1Kr1u5CqBT18T00K3fKHEu89_VD4Du694Mrt7SKtFNM8/edit)
[Priority Queue using Binary Heap - GeeksforGeeks](https://www.geeksforgeeks.org/priority-queue-using-binary-heap/)
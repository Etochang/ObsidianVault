# Homework 4


Premises: 
1. $n >> k$, $1 \le k \le n$: let's assume that $n$ grows faster than $k$. 
2. A1 (Sort All, then Retrieve): 
	1. *Sort* the input array in ascending order, then 
	2. Retrieve and list the last k integers from this sorted array.
3. A2 (BuildHeap, then Extract Max k Times): 
	1. Build a Max-heap out of the input array, and then 
	2. Run the in-place HeapSort for exactly k iterations then return the last k items.
4. A3 (Select the Median-of-Medians Pivot, then Sort the Right Partition): 
	1. Use the linear time Median-of-medians Selection algorithm to find the very k-th largest integer as the pivot, then
	2. Partition the unsorted array with the pivot into two parts, and *sort* the right partition that consists of the k elements larger than or equal to the pivot.

## Part 1

| Algorithm | Step 1        | Step 2          | Justifications                                                                                                                                                                               |
| --------- | ------------- | --------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| A1        | $O(n \log n)$ | $O(k)$          | Step 1 is O($n \log n$) because MergeSort's time complexity is O($n \log n$), and in this situation it is being called on an array of size $n$. Step 2 is just an array retrieval $k$ times. |
| A2        | $O(n)$        | $O(k \log n)$   | Step 1 is O($n$) because Build Heap is O($n$). Step 2 is O($k \log n$) because one iteration of HeapSort has a time complexity of O($\log n$), and there are $k$ iterations.                 |
| A3        | $O(n)$        | $O(n+k \log k)$ | Step 1 is O($n$) because the Selection algorithm is linear time. Step 2 is O($n+k \log k$) because partitioning is O($n$), and MergeSorting $k$ elements is O($k \log k$)                    |

## Part 2

I would choose A2 based on the premise that $n$ is sufficiently larger than $k$, as it lets me assume that $n + k \log k$ grows faster than $k \log n$. Otherwise, I would have trouble picking between A2 and A3, as comparing the time complexities of each algorithm's step 2 would be highly situational. 
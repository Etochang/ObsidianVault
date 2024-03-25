202401290016
Meta Tags: #homework 
Tags: [[CSE 310]] [[recurrence analysis]] [[algorithms]]

# Homework 2

## Part A

Premise: implement a merge operation to **combine 3 sorted subarrays**.
### Pseudocode

```
// parameters are 3 sorted subarrays
int* Merge3(int* arr1, int* arr2, int* arr3) {

	// array to be returned
	int* merged_arr = new int[total # of elements in all three arrays];

	// indexes for arr1, arr2, arr3, and merged_arr respectively
	i1, i2, i3, i_merged = 0;

	while (3 indexes haven't reached the end of their arrays) {
		merged_arr[i_merged] = minimum_of(the three values that each index points to in their own subarray);
		index of subarray with the minimum++;
		i_merged++;
	}

	//This is Merge2()!
	while (2 indexes haven't reached the end of their arrays) {
		merged_arr[i_merged] = minimum_of(the two values that each index points to in the remaining subarrays);
		index of subarray with the minimum++;
		i_merged++;
	}

	while (1 index hasn't reached the end of its array) {
		merged_arr[i_merged] = the value that the remaining index points to in its subarray;
		remaining index++;
		i_merged++;
	}

	return merged_arr;
}
```

## Part B

>Number of subproblems?

 "...and then recursively call MergeSort on all **3 subarrays**" $\implies$  **3** subproblems.

>Size of a subproblem input?

"...per request we now want to split the input array in **3 equal subarrays**..." $\implies$ $n/3$ if input size = $n$.

>Cost of non-recurrent operations?

In the pseudocode, for each number put in the output array:

- At most 3 comparison operations (<=, >,) happen
- two integer incrementations (indexes) happen
- 1 assignment happens (to the output array)

These are all non-dependent on $n$, so the time cost of these operations is $c$. Since there are $n$ numbers in the input array, the total time cost of the non-recurrent operations is $c\cdot n$.  

>[!note]
>The initial declaration costs can be ignored as this is a Big-O analysis. 

Thus,
$$T(n) = 3\cdot T(n/3)+c\cdot  n$$
And using the Master Theorem:
$$T(n) = a T(n/b)+O(n^d) \ \text{for constants} \ a=3, b =3 , d = 1$$
$$\because d = \log_ba \equiv 1 = \log_33$$
$$\therefore T(n) = O(n\log n)$$



---
# *References*
[HW2 Spring 2024 - Google Docs](https://docs.google.com/document/d/1JvM--CUq2Ojn0-joo0uvpQmv_kp1EmMtgZICghOdrxg/edit)
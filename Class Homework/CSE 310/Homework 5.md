# Homework 5

| Operation      | Functionality                                                                                                                                                    |
| -------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Search(D, x)   | Search for x in D, and return True or False whether x exists in D.                                                                                               |
| Insert(D, x)   | Insert a new element x into D, then update D's internal structure accordingly.                                                                                   |
| Delete(D, x)   | Remove an existing element x out of D given x's address, then update D's internal structure accordingly. PS. We don't need to look for x in D in this operation. |
| Extract-MAX(D) | Remove and return the largest element out of D, then update D's structure accordingly.                                                                           |

> List down the **worst-possible running time** per operation for all above three candidates in terms of Big-O-of-N, N being the number of already existing elements in the said data structure. (9 pts) Some of the Big-O solutions are given to you as granted.

| Operation   |                                 Max-Heap                                  |                                          BST                                           |                    Red-Black Tree                     |
| ----------- | :-----------------------------------------------------------------------: | :------------------------------------------------------------------------------------: | :---------------------------------------------------: |
| Search      |                                  $O(N)$                                   |                               $O(N)$<br>*chain shape*\*                                |          $O(\log N)$<br>*self-balancing BST*          |
| Insert      |                                $O(\log N)$                                |                                      $O(N)$<br>\*                                      | $O(\log N)$<br>*rotations are O(1), log N traversals* |
| Delete      |                                $O(\log N)$                                | $O(N)$<br>*finding the in-order successor/predecessor takes linear time in worst case* |       $O(\log N)$<br>*may cascade up the tree*        |
| Extract-MAX | $O(\log N)$<br>*max is already at root; just return root and then delete* |                                      $O(N)$<br>\*                                      |       $O(\log N)$<br>*may cascade up the tree*        |


> If the worst-case running time is the sole concern, which of the above three data structures would you choose that has the best performance? Justify your choice within the blank left below in at most 2 full sentences.  (1 pt) No pseudocode is ever needed.

I would choose the Red-Black tree, because it overall has the lowest worst-case time complexities between the three data structures given.
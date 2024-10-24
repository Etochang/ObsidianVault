202406181853
Meta Tags: #class
Tags: [[OS]]

# Videos - Module 7

## Bounded-Buffer Problem

- N buffers, each can hold one item
- Semaphore mutex initialized to the value 1
	- provides mutual exclusion for accesses to the buffer pool
- Semaphore full initialized to the value 0
	- counts the number of full buffers
- Semaphore empty initialized to the value N
	- counts the number of empty buffers

### Solution

Producer:
```
do {
	//produce an item
	wait(empty);
	wait(mutex);

	//add item to the buffer

	signal(mutex);
	signal(full);
} while(true);
```

Consumer:
```
do{
	wait(full);
	wait(mutex);

	//remove an item from the buffer

	signal(mutex);
	signal(empty);
	//consume the item
} while)true
```

- might still run into deadlocks

## Readers-Writers Problem

- A data set is shared among a number of concurrent processes
	- readers - only read the data set; don't perform any updates
	- writers - can both read and write
- Problem:
	- allow multiple readers to read at the same time
	- but only one single writer can access the shared data at the same time

### Solution

- semaphore mutex initialized to 1
	- provides mutual exclusion for access to readcount
- semaphore wrt initialized to 1
	- provides multual exclusion for the writers (and between writer and reader)
- integer readcount initialized to 0
	- keeps track of how many processes are currently reading

Writer:
```
do {
	wait(wrt);

	//writing is performed

	signal(wrt);
} while(true);
```

Reader:
```
do {
	wait(mutex);
	readcount++;
	if (readcount == 1)
		wait(wrt);
	signal(mutex);

	//reading is performed

	wait(mutex);
	readcount--;
	if(readcount == 0)
		signal(wrt);
	signal(mutex);
} while(true);
```

- This problem is called the "first" readers-writers problem
	- no readers should be waiting unless a writer is already accessing the data
- The "second" readers-writers problem
	- if a writer is waiting to access, no new readers may start reading


---
# *References*
https://canvas.asu.edu/courses/187584/assignments/5154812?module_item_id=13536082
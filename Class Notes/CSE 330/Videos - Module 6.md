202406181644
Meta Tags: #class
Tags: [[OS]]

# Videos - Module 6

## Synchronization Problem

### Background

- Concurrent access to shared data may result in data inconsistency
	- maintaining data consistency requires mechanisms top ensure the orderly execution of cooperating processes
- e.g., shared-memory solution to the consumer-producer problem
	- suppose that we want to improve it so that we can use the entire buffer - we can do so by having an integer count to keep track of the number of full buffers
### Producer

```
while (true) {
	while (count == BUFFER_SIZE) {
		//do nothing
	}
	buffer[in] = nextProduced;
	in = (in + 1) % BUFFER_SIZE;
	count++;
}
```

### Consumer

```
while (true) {
	while (count == 0) {
		//do nothing
	}
	nextConsumer = buffer[out];
	out = (out + 1) % BUFFER_SIZE;
	count--;
}
```

### Race Condition

>count++ could be implemented as:

```
register1 = count
register1++;
count = register1
```

>count-- could be implemented as:

```
register2 = count
register2--;
count = register2
```

If one starts before the other finishes updating count, then count will be either one less or one more than expected, since the one that starts later will work on the previous value of `count`.

>[!info] Definition
>the situation where several processes access and manipulate the same data concurrently and the outcome of the execution depends on the particular order in which the access takes place

>Solution: use process synchronization to ensure that only one process at a time can be manipulating the shared data

## Critical-Section Problem

- **Critical section:** the segment of code in which no two or more processes can execute at the same time
	- where a process can safely manipulate shared data
- **The problem:** to design a protocol that processes can use to cooperate the execution of critical sections
- **Entry section:** the section of code implementing the request of permission of entering its critical section
- **Exit section:** the section of code implementing the exit of critical section

### General Structure of Critical Section

```
do {
	entry section
		critical section
	exit section
		remainder section
} while (true);
```

### Solution to Critical-Section Problem

>[!info] Mutual Exclusion
>If one process is executing in its critical section, then no other processes can be executing in their critical sections

>[!info] Progress
>If no process is executing in its critical section, then the selection of the processes that will enter the critical section next cannot be postponed indefinitely

>[!Info] Bounded Waiting
>A bound must exist on the number of times that other processes are allowed to enter their critical sections while one process is waiting to enter its critical section

- Assume that each process executes at a nonzero speed
- No assumption concerning relative speed of processes

## Peterson's Solution

- Two process solution:
	- classic software-based solution to critical-section problem
	- may not work on modern computer architecture
- The two processes share two variable:
	- int `turn`, indicating whose turn it is to enter the critical section
	- boolean `flag`, indicating if a process is ready to enter the critical section. `flag[i] = true` implies that process $P_i$ is ready

### Algorithm for Process $P_i$ and $P_j$

```
do {
	flag[i] = TRUE; //entry start
	turn = j;
	while (flag[j] && turn == j); //entry end
		critical section
	flag[i] = FALSE; //exit
		remainder section
} while (TRUE);
```
```
do {
	flag[j] = TRUE; //entry start
	turn = i;
	while (flag[i] && turn == i); //entry end
		critical section
	flag[j] = FALSE; //exit
		remainder section
} while (TRUE);
```

## Low-Level Synchronization Tools
### Synchronization Hardware

- many systems provide hardware support for critical section code
- TestAndSet Instruction:

```
boolean TestAndSet (boolean *target) {
	boolean rv = *target;
	*target = TRUE;
	return rv;
}
```

- Executed atomically (cannot be interrupted or interleaved) - two concurrent TestAndSet instructions will be executed sequentially in some arbitrary order

### Mutual Exclusion Using TestAndSet

- shared boolean variable `lock`,  initialized to false:

```
do {
	while(TestAndSet(&lock)) {
		//do nothing
	}
		critical section
	lock = FALSE;
		remainder section
} while(TRUE);
```

### Bounded-Waiting Mutual Exclusion Using TestAndSet

```
do {
	waiting[i] = TRUE;
	key = TRUE;
	while (waiting[i] && key) {
		key = TestAndSet(&lock);
	}
	waiting[i] = FALSE;
	// critical section
	j = (i + 1) % n;
	while ((j != i) && !waiting[j]) {
		j = (j + 1) % n;
	}
	if (j == i) {
		lock = FALSE;
	} else {
		waiting[j] = FALSE;
	}
	// remainder section
} while(TRUE);
```


## High-Level Synchronization Tools

### Mutex Locks

- hardware-based are complicated and inaccessible to application programmers
- OS provides high-level synchronization primitives
- Mutex lock (mutex stands for mutual exclusion)
	- a boolean variable indicating whether the lock is available
	- `acquire()` - acquire the lock if successful
	- `release()` - release the lock

```
acquire() {
	while (!available)
		//busy wait
	available = false;
}

release() {
	available = true;
}
```

>[!info] Busy Waiting
>While a process is in its critical section, any other process that tries to enter its CS must loop continuously in the call to `acquire()`; the same issue exists for the `TestAndSet()` example. The opposite of this is called **sleep waiting**.

This type of mutex lock is also called a spinlock:
- wastes CPU cycles that other processes might be able to use
	- particularly when a single CPU is shared among many processes
- Doesn't require context switch while waiting
	- useful when locks are expected to be held for short times
	- often employed on multiprocessor systems

### Semaphore

- a less complicated synchronization tool
- an integer variable
- accessed only through two standard atomic operations
	- `wait()`, a.k.a. `P()`
	- `signal()`, a.k.a. `V()`

```
wait(S) {
	while (S <= 0)
		//do nothing
	S--;
}

signal(S) {
	S++;
}
```

### Semaphore as General Synchronization Tool

- **Binary Semaphore:**
	- integer value can range only between 0 and 1
	- a.k.a. mutex locks
- **Counting Semaphore:**
	- integer value can range over an unrestricted domain
	- used to control access to a given resource with a finite number of instances
		- initialized to the number of resources available

#### Mutual Exclusion

```
semaphore mutex; //initialized to 1
do {
	wait(mutex);
	//critical section
	signal(mutex);
	//remainder section
} while(true);
```

## Semaphore Implementation

```
wait (S) {
	while S <= 0
		//nothing
	S--;
}
```

This requires busy waiting.

### Without Busy Waiting

With each semaphore, there is an associated waiting queue:

```
typedef struct {
	int value;
	struct process *list;
} semaphore;
```

Two operations:
- block - place the process invoking the operation on the appropriate waiting queue, sends running to waiting
- wakeup - remove one of the processes in the waiting queue and place it in the ready queue, sends waiting to ready

```
wait(semaphore *S) {
	S->value--;
	if(S->value < 0) {
		add this process to S->list;
		block();
	}
}

signal(semaphore *S) {
	S->value++;
	if (S->value <= 0) {
		remove a process P from S->list;
		wakeup(P);
	}
}
```

- If context switch time is significant relative to process completion time, then busy waiting is better than sleep waiting.
- Busy waiting is not completely eliminated, since the wait and signal operations are critical sections themselves that have to be solved by low-level synchronization tools which have to be spinning.

### Deadlock

- two or more processes waiting indefinitely for an event that can be caused by only one of the waiting processes

---
# *References*
https://canvas.asu.edu/courses/187584/assignments/5154825?module_item_id=13536077
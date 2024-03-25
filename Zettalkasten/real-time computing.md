202402110137
Meta Tags: #definition 
Tags: [[embedded systems]]

# real-time computing

**Real-time computing** (RTC) describes hardware and software systems subject to "real-time constraints", i.e. from [[event]] to [[system response]]. These "real-time constraints" also go by the term, *deadlines*. 

A system that is not described as "real-time" cannot *guarantee* a response for any time constraint, though it may have *expected* or *typical* response time estimates. On the other hand, a real-time system **MUST** meet deadlines regardless of [[system load]]. 

>A real-time system has been described as one which "controls an environment by receiving data, processing them, and returning the results sufficiently quickly to affect the environment at that time".

Real-time software may use one or more of the following: [[synchronous programming language|synchronous programming languages]], [[RTOS|RTOSes]],  and real-time networks.

## Criteria for real-time computing

The deadlines of a real-time system are classified by the consequences of missing one:

- *Hard* - missing it is total system failure
- *Firm* - infrequent misses are tolerated, but a usefulness of a miss is $\le 0$ to the overall system
- *Soft* - The usefulness of a result is degraded after the deadline, but is still better than nothing

A **hard** real-time system is one that has to ensure that all deadlines are met, and a **soft** real-time system is one that optimizes usefulness through focusing on specific deadlines.

 

---
# *References*
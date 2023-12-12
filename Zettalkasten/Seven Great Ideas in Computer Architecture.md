202312062125
Meta Tags: #textbook 
Tags: [[computer organization]]

# Seven Great Ideas in Computer Architecture

These are the seven great ideas that computer architects have invented in the last 60 years of computer design:

## Use Abstraction to Simplify Design

Using **abstractions** to represent a design at different levels of representation is a major productivity technique for hardware and software; lower-level details are hidden to offer a simpler model at higher levels. 

![[F000011icon01-9780128201091.jpg]]
## Make the Common Case Fast

Making the **common case fast** will tend to enhance performance better than optimizing the rare case.

![[F000011icon02-9780128201091.jpg]]

## Performance vis Parallelism

Performing operations in parallel will offer more performance.

![[F000011icon07-9780128201091.jpg]]

## Performance via Pipelining

**Pipelining** is a specific type of parallelism. For example, before fire engines, a "bucket brigade" would respond to a fire, a human chain of people passing buckets along to the fire rather than individuals running back and forth.
![[F000011icon08-9780128201091.jpg]]

## Performance via Prediction

In some cases it can be better to guess and start working rather than wait until you know for sure, assuming that your prediction is relatively accurate and the cost to recover from a misprediction is not too expensive.

![[F000011icon09-9780128201091.jpg]]

## Hierarchy of Memories

Have the fastest, smallest, and most expensive memory at the top of the hierarchy and the slowest, largest, and cheapest memory at the bottom. This will give the programmer the illusion that main memory is as fast as the top and as cheap and big as the bottom.

![[F000011icon04-9780128201091.jpg]]

## Dependability via Redundancy

Include redundant components that can take over when a failure occurs *and* to help detect failures.

![[F000011icon03-9780128201091.jpg]]

>[!important] Elaboration
>During the heydays of Moore’s Law, the cost per chip resource would drop with each new technology generation. In the latest technologies, the cost per resource may be flat or even _rising_ with each new generation, due to the cost of the new equipment, the elaborate processes invented to make chips work at these finer feature sizes, and the reduction of the _number_ of companies who are investing in these new technologies to push the state-of-the-art. Less competition naturally leads to higher prices.

# [[Below Your Program]]

---
# *References*
202406161805
Meta Tags: #class 
Tags: [[software engineering]]

# Introduction to Design Patterns

## Why Design Patterns❔

- a design pattern represents a **reusable solution** to a commonly occurring problem in software design
- design patterns are proven solutions under certain software requirements
- Such design patterns improve the body of knowledge of software design so that proven solutions can be **adopted** with required modifications (if needed) in solving a new problem
- Benefits:
	- improved modularity
	- better testability using known techniques
	- assure software quality attributes that can be derived from known patterns
	- etc.

## Software Design Patterns among Overall Software Design Activities

![[Pasted image 20240616180931.png]]

**Domain Analysis, Requirements Analysis, Risk Analysis:** 
- Gives analysis-level artifacts:
	- use cases
	- use-case diagrams
	- class diagrams

**Hardware Architecture Design:**
- Gives deployment diagram

## Categories of Object-Oriented Design Patterns

![[Pasted image 20240616181233.png]]

## Creational Design Patterns

- main objective: provide different techniques to instantiate and create objects instances efficiently
- improves factors like:
	- runtime resource usage
	- modularity/modifiability of the design
	- testability of the system
	- etc.

Types:
![[Pasted image 20240616181851.png]]

### Factory Design Pattern

- Rather than the client creating different types of object instances, it uses the service of an object factory to request the type of object instance needed.

![[Pasted image 20240616182016.png]]

### Abstract Factory Design

- provides an interface to create a group of individual factories with common theme without specifying their concrete classes

### Prototype Design Pattern

- provides a prototype of the object (initial setup) that can be copied/cloned. This will remove the need of object initialization process repeatedly.

### Singleton Design Pattern

- class in which only single instance is possible. In a software system, sometimes we need objects for which only one instances is needed as it may represent system configuration or universal set of attributes/methods that all the other objects utilize.

![[Pasted image 20240616182354.png]]

### Builder Design Pattern

- aims to separate the construction of a complex object from its representation. The same construction process can be used to create different representations.

![[Pasted image 20240616182556.png]]

### Object Pool Design Pattern

- has a collection of object instances where clients can request them. Once an object instance is assigned to a client it will no longer be available until returned. This pattern is used in situations where cost of initializing the class is very high so there is a limited number of instances.

## Behavioral Design Patterns

- are about identifying common communication pattern between objects. Essentially, these patterns provide a body of knowledge that represents **how objects interact with each other**.
- maintain modularity while establishing communication

![[Pasted image 20240616183040.png]]

### Chain of Responsibility Design Pattern

- way of passing requests among multiple participating objects in the system. The client isn't aware of this chain of responsibility.

![[Pasted image 20240616183518.png]]

![[Pasted image 20240616183508.png]]

### Observer Design Pattern

- Change in one object will be notified to other relevant objects. Notification mechanisms vary in different programming languages.

![[Pasted image 20240616183145.png]]

### Strategy Design Pattern

- some application require different algorithms to be executed at different times and the determination is done at runtime. In order to facilitate such requirements, the Strategy pattern implements a collection of algorithms as objects so that the application can select the suitable object at runtime.

### Iterator Design Pattern

- sequentially access items in the collection without using the implementation of the collection
- provides access to elements in the collection using operations such as next(), previous()

![[Pasted image 20240616183349.png]]

### State Design Pattern

- State of object is represented as another object. As the state of the object changes, state behavior of the object-implementation object is called. Easy to add different states

![[Pasted image 20240616183638.png]]

### Visitor Design Pattern

- used when we have to perform an operation on a group of similar kinds of objects; we can move the operation logic (algorithms) from the objects to another class. 

### Mediator Design Pattern

- a communication bus that controls how different objects interact with each other. This reduces the coupling among objects in the expense of developing a separate mediator object.

![[Pasted image 20240616183817.png]]





---
# *References*
https://canvas.asu.edu/courses/185762/assignments/5104404?module_item_id=13399379

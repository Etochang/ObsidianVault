202406091755
Meta Tags: #class
Tags: [[software engineering]]

# Object Oriented Analysis and Modeling

## Identifying Objects - Approach

![[Pasted image 20240609175742.png]]

## Identifying and Modeling Objects
![[Pasted image 20240609175805.png]]

- The main outcome from this process is the identification of objects and their relationships starting from use-case scenarios

## Categorization of Classes

- boundary - classes that interact with entities outside of the system (UI, database, API, OS, etc.)
	- Serves as an interface between the system and its environment 
	- reduces complexity (minimizes communication and coordination between other classes and the actors by providing an interface neutral form of communication)
	- helps maintainability (normally only boundary class will need to change when interface changes)
- entity - classes that contain all the data, procedures, algorithms, etc. All the computations + internal database operations
	- Are independent of the system's interfaces
	- Correspond to real-world entities that the system manipulates 
	- Represents computations, algorithms and data
	- "Heart of the system"
- control - interface between boundary and entity classes
	- Responsible for coordinating boundary and entity classes
	- Receives/handles system events
	- Often one control class per use case
	- Control classes encapsulate behavior of use case
	- Often one control class represents data validation from user inputs, directing/coordinating system functionality execution, direct actions related to events ...etc

This categorization represents a separation of concerns that supports maintainability and minimizes complexity

## Identifying Object Classes

>[!info] External entities
>Other systems, device, people, etc. that produce or consume information to be used by a computer-based system

>[!info] Things
>Reports, displays, letters, signals, etc. that are part of the information domain for the problem

>[!info] Occurrences or events
>A property transfer/completion of a series of robot movements, etc. that occur within the context of system operation.

## Analysis Classes

- **Roles** - (e.g. manager, engineer, salesperson) played by people who interact with the system
- **Organizational units** - (e.g. division, group, team) that are relevant to an application
- **Places** - (e.g. manufacturing floor or loading dock) that establish the context of the problem and the overall function of the system
- **Structures** - (e.g. sensors, vehicles, or computers) that define a class of objects or related classes of objects

## Defining Operations

- manipulate data in some way
- perform a computation
- inquire about the state of an object
- monitor an object for the occurrence of a controlling event
- Grammatical phrases - verbs

## CRC Diagrams and Class Diagrams

After object identification, make a CRC Diagram.

CRC diagram represents the responsibilities (functions) of each class and other collaborating classes to achieve those functionalities.

Class diagrams describe static structure of the system, objects/classes including attributes and operations, and relationship among them.

### CRC Diagrams

are like an index card set where each index card has three portions:
- **Class:** name of the class and a description of the class indicating main functionality
- **Responsibility:** lists main functionalities of the class
- **Collaborator:** collaborator classes for each functionality (if any)

## From Use-Case Diagrams to CRC

- Use-case diagram represents the high-level dynamic view of the system. It depicts main functionalities, their relationship, and entities (actors) that invoke these functionalities. Use-case diagram doesn't show how functionalities will be implemented.

## Object Representation

### Class Diagram Format

![[Pasted image 20240609183007.png]]

- each member of a class (attribute or method) has a level of visibility
	- public - accessible by all other methods
	- private - accessible by methods within the class
	- protected - accessible by methods of the class and its subclasses
- UML notation
	- +
	- -
	- \#



---
# *References*
https://canvas.asu.edu/courses/185762/assignments/5104421?module_item_id=13399354
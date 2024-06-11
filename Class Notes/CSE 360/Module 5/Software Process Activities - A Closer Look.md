202406081519
Meta Tags: #class
Tags: [[software engineering]]

# Software Process Activities - A Closer Look

## Quick Review

- Real software processes are interleaved sequences of technical, collaborative and managerial activities with the overall goal of specifying, designing, implementing, and testing a software system.
	- Specification (requirement engineering)
	- development (design and implementation)
	- validation
	- evolution

## Software Specification and Requirement Engineering Process

![[Pasted image 20240608154807.png]]

- Requirements Specification: defining the requirements in detail
- Requirements Validation: checking the validity of the requirements

- System Descriptions: UI Walkthrough, deployment diagram (how different components are deployed in the prime time environment)
- User and System Requirements: User Stories, Use Cases/Use Case Diagrams, SRS document
- Requirements Document: contains everything

## Design and Implementation

![[Pasted image 20240608155527.png]]

- Requirements Specification - essentially tells us what are the major functional/nonfunctional requirements
- Data Description - what kind of data is needed in our system? How will it be interacted with? How is data structured to satisfy those interactions?
- Platform Information - How we are going to deploy the software in the runtime environment: OS, protocols, etc.

Design Activities:
- Architectural Design - starting from software architecture, 'floor plan', what are the main components of the system and how do they interact with each other? What kind of interfaces do we have and how will we deploy the components?
	- Identify the overall structure of the system, the principal components (subsystems/modules), their relationships and how they are distributed
- Interface Design - How do we design the interfaces between the components (protocols, UI etc.)
	- Where you define the interfaces between system components
- Component Design - How do we design each component? Identifying objects, establishing relationships between objects (class diagrams)
	- Where you search for reusable components, if unavailable, you design how it will operate.
- Database Design - What database system is being used? How will this be implemented in terms of the architecture and components?
	- Where you design the system data structures and how they will be represented in a database.

Design Outputs:
- System Architecture
	- Deployment Diagram
	- Interaction Diagram
 - Database Specification
	 - what are the data entities
	 - what are the attributes we need to have in each of these
	 - how are these data entities related to each other
	 - How is data stored in the system?
	 - E-R Diagram (Entity-Relationship Diagram)
 - Interface Specification
	 - How will the UI and other interfaces look like?
	 - Component Diagram
 - Component Specification
	 - Class Diagram

## System Implementation

- The software is implemented either by developing a program or programs or by configuring an application system
- Design and implementation are interleaved activities for most types of software systems (+ testing as well)
- Programming is an individual activity with no standard process
- Unit testing (integration testing) and debugging is also an integral part of this process that involves finding program faults and correcting these faults

## Software Verification and Validation

- V&V is intended to show that a system **conforms to its specification** and **meets the requirements of the system customer**
- involves **checking and review processes** and **system testing**
- system testing involves executing the system with test cases that are derived from the specification of the real data to be processed by the system
- testing is the most commonly used V&V activity

![[Pasted image 20240608161241.png]]

### Testing Stages

- Component testing
	- individual components are tested independently
	- components may be function or objects or coherent groupings of these entities
	- JUnit, Nunit, DBunit
- System testing
	- testing of the system as a whole. Testing of system states, component level interactions are particularly important
	- state diagrams, sequence diagrams, interaction diagrams
- Customer/Acceptance testing
	- testing with customer data to check that the system meets the customers' needs
	- use case based testing, random testing

## Testing phases in a plan-driven software process (V-model)

![[Pasted image 20240608161649.png]]

## Software Evolution

- As requirements change, the software must also evolve and change
- Although there has been a demarcation between development and evolution (maintenance) this is increasingly irrelevant as fewer and fewer systems are completely new

![[Pasted image 20240608162014.png]]


---
# *References*
https://canvas.asu.edu/courses/185762/assignments/5104439?module_item_id=13399335
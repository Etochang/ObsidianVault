202406162130
Meta Tags: #class
Tags: [[software engineering]]

# Software Architecture

## Architectural Representations

- simple, informal block diagrams showing entities and relationships are the most frequently used method for documenting software architectures
	- these have been criticized because they lack semantics, don't show the types of relationships between entities nor the visible properties of entities in the architecture
	- very abstract - doesn't show the nature of component relationships nor the externally visible properties of the sub-systems
	- useful for communication with stakeholders and for project planning

- **C4 Approach:** 
	- L1 - Context: the highest level of abstraction. Shows the entire system as a single box and describes who and what interacts with the system from the outside.
	- L2 - Containers: individual components of our software that can be executed and deployed; need to be running for the whole system to operate.
	- L3 - Components: zoom in to each container, and see the individual modules.
	- L4 - Code: zoom in to each module and see the implementation
	- Deployment View: Hardware and Software for the containers/components

"a component is a grouping of related functionality encapsulated behind a well-defined interface."

## Design Decisions

- architectural design is a creative process, so the process differs depending on the type of system being developed
- however, a number of common decisions span all designs and affect all non-functional requirements

1. Is there a generic application architecture that can act as a template for the system that is being designed?
2. How will the system be distributed across hardware cores/processors?
3. What architectural patterns or styles might be used?
4. What strategy will be used to control the operation of the components in the system?
5. How should the architecture of the system be documented?
6. What architectural organization is best for delivering the non-functional requirements of the system?
7. How will the structural components in the system be decomposed into sub-components?
8. What will be the fundamental approach used to structure the system?

## Architectural Reuse

- systems in the same domain often have similar architectures that reflect domain concepts.
- application product lines are built around a core architecture
- the architecture of a system may be designed around one or more architectural patterns/styles.

## Architecture and System Characteristics

- Performance: localize critical operations and minimize communications. Use large rather than fine-grain components
- Security: use a layered architecture with critical assets in the inner layers
- Safety: localize safety-critical features in a small number of sub-systems
- Availability: include redundant components/mechanisms for fault tolerance
- Maintainability: use fine-grain, replaceable components
	- coupling: more equals more connections (Less)
	- cohesion: more equals more independence from other modules (More)

## Service-Oriented Computing

### Types of Web Services

- services are loosely coupled, reusable components that encapsulate discrete functionality, which may be distributed and programmatically accessed. 
- a web service is a service that is accessed using standard Internet and XML-based protocols

- services are platform and implementation-language independent
- two types of web services: SOAP (Simple Object Access Protocol, runs on top of HTTP) and REST (directly work on HTTP, less payload)

### SOAP Web Service Structure

![[Pasted image 20240616222738.png]]

### REST Web Service Structure

![[Pasted image 20240616223122.png]]

### Benefits

- services can be offered by any service provider inside or outside of an organization so organizations can create applications by integrating services from a range of providers
- the service provider makes information about the service public so that any authorized user can use the service
- applications can delay the binding of services until they are deployed or until execution; this means that applications can be reactive and adapt their operation to cope with changes to their execution environment

![[Pasted image 20240616223411.png]]








---
# *References*
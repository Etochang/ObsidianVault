202406162118
Meta Tags: #class
Tags: [[software engineering]]

# Introduction to Software Architecture

## Architectural Design

- concerned with designing the overall structure of the system. 'The organization'.
- provides the critical link between requirements engineering and the design, as it identifies the main structural components in a system and the relationships between them.
- in the small, it is concerned with the architecture of individual programs. At this level, we are concerned with the way that an individual program is decomposed into components.
- in the large, it is concerned with the architecture of complex enterprise systems that include other systems, programs, and components. These systems are distributed over different computers, which may be owned and managed by different companies.

## Architectural Views

- What views/perspectives are useful when designing and documenting a system's architecture?
- What notations should be used for describing architectural models?
- Each architectural model only shows one view or perspective of the system.
	- it might show how a system is decomposed into modules, how the run-time processes interact or the different ways in which system components are distributed across a network. For both design and documentation, you usually need to present multiple view of the software architecture

**Logical View:** shows the key abstractions in the system as objects - class diagrams
**Process View:** shows how, at run-time, the system is composed of interacting processes - sequence diagrams, interaction diagrams
**Development View:** shows how the software is decomposed for development - component bills
**Physical View:** shows the system hardware and how software components are distributed across the processors in the system - deployment diagrams

Use cases/scenarios can be thought of as an extra view as well.

## Advantages of Explicit Architecture

- Stakeholder communication
	- architecture may be used as a focus of discussion
- System analysis
	- means that analysis of whether the system can meet its non-functional requirements is possible; also produces a complete system model that shows the different components in a system, their interfaces and their connections
- Large-scale reuse
	- architecture may be reusable across a range of systems



---
# *References*
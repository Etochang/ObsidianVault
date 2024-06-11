202406081628
Meta Tags: #class
Tags: [[software engineering]]

# Software Requirement Engineering

## System Requirements

- The system requirements are generated during the requirements engineering process
	- the process of establishing the system features that customer requires from a system and the constraints under which it operates and is developed
- In addition to identifying system features/constraints, requirement specifications in various forms help communicate with **stakeholders** (any person/organization who is affected by the system in some way, and anyone who has a legitimate interest)
	- end users
	- system managers
	- software engineers/developers
	- system owners
	- external stakeholders

## Functional and Non-functional Requirements

>[!info] Functional
>- Statements of functionalities/features that the system should provide, how the system should react to particular inputs and how the system should behave in particular situations
>- Basically, what the system should and shouldn't do

>[!info] Non-functional
>- Constraints on the functionalities offered by the system such as timing constraints, constraints on the development process, standards, etc.
>- Often apply to the system as a whole rather than individual features or services

## Functional Requirements

- Describe system features
- **user requirements** - high-level statements of what the system should do
- **system requirements** - should describe the system features in detail, what and how
- Depends on the type of software, expected users and the type of system where they software is used.

### Requirements Imprecision

- Problems arise when functional requirements aren't precisely stated
- Ambiguous requirements may be interpreted in different ways by developers and users
- User intention vs. Developer intention
- Use feedback to get rid of this.

### Requirements Completeness and Consistency

- In principle, requirements should be both complete and consistent.
	- Complete - should include descriptions of all facilities required
	- Consistent - should be no conflicts or contradictions in the descriptions of the system facilities
- In practice, because of system and environmental complexity, it is impossible to produce a complete and consistent requirements document

## Non-functional Requirements

- These define system properties and constraints associated with they system e.g. reliability, response time, storage requirements, I/O device capability, system representations, etc.
- **Product requirements** - specify that the product must behave in a particular way e.g. execution speed, reliability, etc.
- **Organizational requirements** - are a consequence of organizational policies and procedures e.g. process standards used, implementation requirements, etc.
- **External requirements** - arise from factors which are external to the system and its development process e.g. interoperability requirements, legislative requirements, etc.

### Types

![[Pasted image 20240608164038.png]]

- Product Requirements - quality factors
	- Usability Requirements - how easy it is to use/learn the software/system
	- Efficiency Requirements
		- Performance Requirements - time performance
		- Space Requirements - storage performance
	- Dependability Requirements - how robust and reliable
	- Security Requirements - how secure
- Organizational Requirements
	- Environmental Requirements
	- Operational Requirements
	- Development Requirements
- External Requirements
	- Regulatory Requirements
	- Ethical Requirements
	- Legislative Requirements
		- Accounting Requirements
		- Safety/Security Requirements

### Implementation

- non-functional requirements may affect the overall architecture of a system rather than the individual components
	- For example, to ensure that performance requirements are met, you may have to organize the system to minimize communications between components.
- A single non-functional requirement, such as a security requirements, may generate a number of related functional requirements that define system services that are required
	- It may also generate requirements that restrict existing requirements

### Metrics for Specifying Non-functional Requirements

![[Pasted image 20240608165202.png]]

## Software Quality Considerations and Quality Frameworks

## Software Quality Concerns

![[Pasted image 20240608170033.png]]

"**Quality**" focus is the foundation. This is how we meet functional and non-functional requirements.

## ISO - 25010 Software Quality Framework

![[Pasted image 20240608170151.png]]

## Quantifiable and Measurable Quality Factors

![[Pasted image 20240608170406.png]]

## Requirement Elicitation - Gathering Requirements

### Requirements Engineering Processes

- The processes used for requirement engineering (RE) vary widely depending on the application domain, the people involved and the organization developing the requirements
- However, there are a number of generic activities common to all processes
	- Requirements elecitation
	- Requirements analysis/specification
	- Requirements validation
	- Requirements management
- In practice, RE is an iterative activity in which these processes are interleaved

![[Pasted image 20240608171702.png]]

### Requirements Elicitation

- Software engineers work with a range of system stakeholders to find out about the application domain, the services that the system should provide, the require system performance, hardware constraints, other systems, etc.

![[Pasted image 20240608171947.png]]

### Problems of Requirements Elicitation
- Stakeholders don't know what they really want
- Stakeholders express requirements in their own terms
- Different stakeholders may have conflicting requirements
- Organizational and political factors may influence the system requirements
- The requirements change during the analysis process. New stakeholders may emerge and the business environment may change.

### Requirements Discovery

- The process of gathering info about the required and existing systems and distilling the user and system requirements from this info.
- Interaction is with system stakeholders from managers to external regulators
- Systems normally have a range of stakeholders

#### Interviewing

- Formal/informal interviews with stakeholders are part of most RE processes
- Types:
	- Closed interviews based on predetermined list of questions
	- Open interviews where various issues are explored w/ stakeholders
- Effective Interviewing:
	- Be open-minded, avoid preconceived ideas about the requirements - no leading questions
	- Prompt the interviewee to get discussions going using a springboard question, a requirements proposal, or by working together on a prototype system

##### Interviews in Practice

- Normally a mix of closed and open-ended interviewing
- Interviews are good for getting an overall understanding of what stakeholders do and how they might interact with the system .
- Interviewers need to be open-minded without pre-conceived ideas of what the system should do
- You need to prompt the use to talk about the system by suggesting requirements rather than simply asking them what they want

##### Problems with Interviews

- Application specialists may use language to describe their work that isn't easy for the requirements engineer to understand
- Interviews aren't good for understanding domain requirements
	- Requirements engineers cannot understand specific domain terminology
	- Some domain knowledge is so familiar that people find it hard to articulate or think that it isn't worth articulating

#### Ethnography

- A social scientist spends a considerable time observing and analyzing how people actually work
- People don't have to explain or articulate their work
- social and organizational factors of importance may be observed
- Ethnographic studies have shown that work is usually richer and more complex than suggested by simple system models

##### Scope

- Requirements that are derived from the way that people actually work rather than the way which process definitions suggest that they ought to work
- Requirements that are derived from cooperation and awareness of other people's activities
	- Awareness of what other people are doing leads to changes in the ways in which we do things
- Ethnography is effective for understanding existing processes but cannot identify new features that should be added to a system

### Stories and Scenarios - Requirements Specification

- Scenarios and user stories are real-life examples of how a system can be used
- Stories and scenarios are a description of how a system may be used for a particular task
- Because they are based on a practical situation, stakeholders can relate to them and can comment on their situation with respect to the story

## Requirements Elicitation - Documenting Requirements

### Ways of Writing a System Requirements Specification (SRS)

![[Pasted image 20240608173544.png]]

### Use-Case Based Representation of Requirements

- Key Components:
	- Use-cases: a use case representations of a distinct business functionality in a system; one distinct functionality, major use, should represent a verb
	- Actors: an actor performs key roles in a given system. An actor in a use case diagram interacts with a use case.
	- Use-case diagrams: shows how actors interact with use-cases, relationship among actors, as well as relationship among use-cases
	- Use-case scenarios: a narrative that describes activities associated with the use-case

### Use-Case Diagram Relationships

- **Includes/uses:** when a use-case is depicted as using the functionality of another use-case in a diagram, this relationship between the use-cases is named as an include relationship. Literally speaking, in an include relationship, a use-case includes the functionality described in the other use-case as a part of its business process flow
- **Extends:** the child-use case adds to the existing functionality and characteristics of the parent use-case. An extended use-case may invoke based on certain conditions. "may involve the usage of". Parent is the origin of the arrow
- **Generalization:** is also a parent-child relationship between use cases. The child use-case in the generalization relationship has the underlying business process meaning, but is an enhancement of the parent use-case. Parent is the end of the arrow. Not dotted like others.


1. Find actors
2. Find main functions of actors and system

![[Pasted image 20240608182746.png]]

Use case scenario above.

---
# *References*
https://canvas.asu.edu/courses/185762/assignments/5104445?module_item_id=13399338
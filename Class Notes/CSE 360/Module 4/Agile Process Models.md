202406021912
Meta Tags: #class
Tags: [[process model]] [[software engineering]]

# Agile Process Models

## Reality of Current Software Requirements

- Requirements for many small/medium size software systems increase.
- Dynamic nature of software requirements makes software development more challenging
- **What makes software requirements change:**
	- Changes in team members
	- Changes in software being built
	- Changes because of new tech

## Agile Manifesto

![[Pasted image 20240602191418.png]]

- Individuals and interactions over processes and tools
- Working software over comprehensive documentation
- customer collaboration over contract negotiation
- Responding to change over following a plan

## How to Respond Successfully to Software Requirement Changes❔

- Effective (rapid and adaptive) response to change
- Effective communication among all stakeholders
- Drawing the customer onto the team
- Organizing a team so that it is in control of the work performed
- Rapid, incremental delivery of software

>The aim of agile methods is to reduce overheads in the software process (e.g. by limiting documentation) and to be able to respond quickly to changing requirements without excessive rework.

## Principles

![[Pasted image 20240602191810.png]]

## Applicability

- Product development for a small/medium-sized product for sale
- Custom system development within an organization: clear commitment from the customer to become involved in the dev process and where there are few external rules and regulations that affect the software

XP, Scrum, Kanban

# XP

## Extreme Programming

- Most widely used agile process
- Takes an 'extreme' approach to iterative development
	- New versions may be built several times per day
	- Increments are delivered to customers every 2 weeks
	- All test must be run for every build and the build is only accepted if tests run successfully

![[Pasted image 20240602192222.png]]

- XP Planning
	- Begins with the creation of "user stories"
	- Agile team assesses each story and assigns a cost
	- Stories are grouped to for a deliverable increment
	- A commitment is made on delivery date
	- After the first increment "project velocity" is used to help define subsequent delivery dates for other increments
- XP Design
	- Simple Designs (CRC cards) w/ class responsibility collaborator cards
	- KIS (Keep it Simple principle)
	- For difficult design problems, suggests the creation of spike solutions (prototypes)
	- Encourages refactoring - an iterative refinement of the internal program design
- XP Coding
	- Pair programming
	- Unit testing before coding commences
	- Continuous Integration
	- iterative refactoring
	- collective ownership
	- sustainable pace
- XP Test
	- Acceptance testing is defined by the customer and executed to assess customer visible functionality
	- Unit testing is executed daily
	- Continuous Integration
- XP Release
	- Software Increment
	- Project Velocity Computed

## User Stories for Requirements
- In XP, a customer or user is part of the XP team and is responsible for making decisions on requirements.
- User requirements are expressed as user stories or scenarios
- These are written on cards and the development team break them down into implementation tasks. These tasks are the basis of schedule and cost estimates
- The customer chooses the stories for inclusion in the next release based on their priorities and the schedule estimates

- Stories -> Tasks - Tests w/ I/O

## Practices

![[Pasted image 20240602193239.png]]
![[Pasted image 20240602193318.png]]

## Problems

- Can be difficult to keep the interest of customers who are involved in the process
- Team members may be unsuited to the intense involvement that characterizes agile methods
- Prioritizing changes can be difficult where there are multiple stakeholders.
- Maintaining simplicity requires extra work.

# Scrum

- The principal responsibility of software project managers is to ensure the software is delivered on time and within budget.
- The standard approach to project management is plan-driven. Managers draw up a plan showing what should be delivered, when it should be delivered, and who will work on the development
- Agile project management requires a different approach, which is adapted to incremental development and the practices used in agile methods

>Scrum is an agile method that focuses on managing iterative rather than specific agile practices

- Three phases
	- The initial phase is an outline planning phase where you establish the general objectives for the project and design the software architecture
	- This is followed by a series of sprint cycles, where each cycle develops an increment of the system
	- The project closure phase wraps up the project, completes required documentation such as system help frames and user manuals and assesses the lessons learned from the project.

## Scrum terminology

![[Pasted image 20240602194843.png]]
![[Pasted image 20240602195219.png]]

## Scrum Process

![[Pasted image 20240602195311.png]]

## Scrum sprint cycle

- Sprints are fixed length, normally 2-4 weeks
- The starting point for planning in the product backlog, which is the list of work to be done on the project.
- The selection phase involves all of the project team who work with the customer to select the features and functionality from the product backlog to be developed during the sprint
- Once these are agreed, the team organizes themselves to develop the software
- During this stage, the team is isolated from the customer and the organization, with all communications channeled through the so-called 'Scrum master'.
- The role of the Scrum master is to protect the development team from external distractions
- At the end of the sprint, the work done is reviewed and presented to stakeholders. The next sprint cycle then begins.

## Teamwork

- The scrummaster is a facilitator who arranges daily meetings, tracks the backlog of work to be done, records decisions, measures progress against the backlog and communicates with customers and management outside of the team.
- The whole team attends scrums (daily meetings) where all team members share info, describe their progress, problems that have arisen and what is planned for the following day

## Benefits

- The product is broken down into a set of manageable and understandable chunks
- Unstable requirements don't hold up progress
- the whole team has visibility of everything and consequently team communication is improved
- customers see on-time delivery of increments and gain feedback on how the product works
- Trust between customers and developers is established and a positive culture is created in which everyone expects the project to succeed.

---
# *References*
https://canvas.asu.edu/courses/185762/assignments/5104378?module_item_id=13399322
202406232016
Meta Tags: #class
Tags: [[software engineering]]

# Software Testing

## Introduction

### What Testing Shows

- testing is intended to show that a program does what it is intended to do and to discover program defects before it is put into use
- when you test software, you execute a program using artificial data/real data
- you check the results of the test run for errors, anomalies or information about the program's non-functional attributes
- can reveal the presence of errors NOT their absence
- testing is part of a more general V&V process, which also includes static validation techniques

Goals:
- to demonstrate to the developer and the customer that the software meets its requirements
- to discover situations in which the behavior of the software is incorrect, undesirable, or doesn't conform to its specification

Defect testing is concerned with rooting out undesirable system behavior such as system crashes, unwanted interactions with other systems, incorrect computations and data corruption.

### Who Tests❔

- **Developer:** understands the system, will test "gently", driven by "delivery"
- **Independent Tester:** must learn about the system, will attempt to break it and is driven by quality

### Verification and Validation

- Verification - refers to the set of activities that ensure that software correctly implements a specific function: "are we building the product right?"
- Validation - refers to a different set of activities that ensure that the software that has been built is traceable to customer requirements: "are we building the right product?"

### Testing Strategies

![[Pasted image 20240623202121.png]]

- unit testing - the smallest possible unit in a system (function, object, module, etc.)
- integration testing - integrate the objects into one module and test that, repeat for bigger systems as well
- system testing - how do we test the integrated testing
- validation testing - functionality testing, use-case

### Testing Approaches

**Blackbox Testing:**
- Equivalent Partitioning
- Boundary Value Analysis
- Use-case based testing
- Exploratory testing
- Model-based testing
- Input → Output testing

**Whitebox Testing:**
- Control Flow testing
- Dataflow testing
- Slicing
- Decision to Decision testing

In addition to testing, inspections and reviews are two other commonly used software QA techniques

## Inspections and Reviews

**Software Inspections:**
- involve people examining the source representation with the aim of discovering anomalies and defects
- inspections don't require execution
- may be applied to any representation of the system (requirements, design, configuration data, test data, etc.)
- have been shown to be effective

**Review:**
- IEEE standard for software reviews identify five types:
	- Management Reviews
	- Technical Reviews
	- Inspections
	- Walk-throughs
	- Audits
- Review requirements, specification, design, code, user guides, test cases, etc.

**Management Review:** a systematic evaluation of a software acquisition, supply, development, operation, or maintenance process performed by or on behalf of management that monitors progress, determines the status of plans and schedules, confirms requirements and their system allocation, or evaluates the effectiveness of management approaches used to achieve fitness for purpose

**Technical Review:** evaluate the product to determine its suitability for its intended use. Identify discrepancies from specification and standards.

**Inspections:** evaluation technique in which software requirements, design, or code are examined in detail by person or group other than the author.
\
**Walkthrough:** the author of the code formally presents the requirements, design, or code to a small group of reviewers.

**Audit:** independent examination of a software product, process, or set of software processes to assess compliance with specification, standards, contractual agreements, or other criteria.

![[Pasted image 20240623203151.png]]

**Advantages of Inspections:**
- during testing, errors can mask other errors. Because inspection is  a static process, you don't have to be concerned with interactions between errors
- incomplete versions of a system can be inspected without additional costs
- an inspection can also consider broader quality attributes like maintainability, portability, and compliance with standards

![[Pasted image 20240623203326.png]]

## Blackbox Testing

![[Pasted image 20240623203422.png]]

- don't know what is inside
- know how to run the system, and types of inputs and outputs

**Equivalent Partitioning:** divides the input domain of a program into classes of data from which test cases can be derived. It strives to define a test case that uncovers classes of errors, and reduces the total number of testcases.

![[Pasted image 20240623203645.png]]

Guidelines:
- if input specifies a range
	- one valid value
	- two invalid values
- if input requires specific value
	- one valid value
	- two invalid values
- if input specifies a member of a set
	- one valid (in a set)
	- one invalid (not in a set)
- if input condition if Boolean
	- one valid
	- one invalid

![[Pasted image 20240623203911.png]]


**Boundary Value Analysis:**
- a greater number of errors occurs at the boundaries of the input domain rather than in the "center".
- it complements equivalence partitioning

Example:
- if an input condition specifies a range bounded by values a and b, test cases should be:
	- values a and b
	- just above and just below a and b

## Use-Case Based Testing

![[Pasted image 20240623204220.png]]

- use case basic flow and alternative flows provide sequence of events and actions related to the use case and system output
- thus, use case scenarios provide a set of steps in testing the application







---
# *References*
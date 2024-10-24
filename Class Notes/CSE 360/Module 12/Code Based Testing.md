202406281641
Meta Tags: #class
Tags: [[software engineering]]

# Code Based Testing

## White-Box Testing

### Unit Testing

- the process of testing individual components in isolation
- a defect testing process
- units may be:
	- individual functions or methods within an object
	- object classes with several attributes and methods
	- composite components with defined interfaces used to access their functionality

### Object Class Testing

- Complete test coverage of a class involves
	- testing all operations associated with an object
	- setting and interrogating all object attributes
	- exercising the object in all possible states
- Inheritance makes it more difficult to design object class tests as the information to be tested is not localized

Example:

![[Pasted image 20240628165552.png]]

- need to define test cases for reportWeather, calibrate, test, startup, shutdown, etc.
- using a state model, identify sequences of state transitions to be tested and the event sequences to cause these transitions
	- Shutdown → Running → Shutdown
	- Configuring → Running → Testing → Transmitting → Running
	- Running → Collecting → Running → Summarizing → Transmitting → Running

### Different Approaches

- Control Flow - 'trace' the program pointer 
- Dataflow - monitor the data values of interest
- Slicing
- Decision to Decision
- etc.

### Basic Approach

- involves developing test cases and testing the software system based on the code
- thus, the tester has access to the code and is knowledgeable about the programming language used to develop the software
- code-based testing focus on covering the code in various angles - test coverage

**Code-based testing strategies:**
1. Statement coverage
2. Basic path testing (control flow coverage)
3. Decision-to-Decision testing
4. Dataflow coverage
5. Condition testing
6. Code-based risk assessments (complexity, object oriented matrices, etc.)

Most of these testing techniques see the program as a graph.

![[Pasted image 20240628170359.png]]

1 is the source, and 7 is the sink.

If the graph has one source node and one sink node, then we can apply the equation for cyclomatic complexity. 

## JUnit

From the test cases of the previous control flow graph, we can make a separate java class and import JUnit libraries like this:

```
import static org.junit.Assert.*;
import org.junit.Test;

public class Test {

@Test
public void T1() {
	assertEquals(1, a.doSomeThing(1,1));
}

@Test
public void T2() {
	assertEquals(1, a.doSomeThing(1,2));
}

@Test
public void T3() {
	assertEquals(1, a.doSomeThing(2,1));
}

}
```

- JUnit is a single framework to write repeatable tests. It is an instance of the xUnit architecture for unit testing frameworks written by Kent Beck and Erich Gamma

### What is a Framework❔

- A framework is a semi-complete application
- it provides a reusable, common structure to share among applications
- developers incorporate the framework into their own application and extend it to meet their specific needs
- frameworks differ from toolkits by providing a coherent structure, rather than a simple set of utility classes

### Framework Elements

- TestCase
	- Base calss for classes that contain tests
- assert*()
	- Method family to check conditions
- TestSuite
	- Enables grouping several test cases

### JUnit and Class Testing

- In addition to @Test, JUnit annotations to provide resource initialization and reclamation methods include: @Before, @BeforeClass, @After, @AfterClass, etc.
- A variety of assert methods to make it easy to check the results of your tests
- Integration with popular IDEs

## Control Flow Graph Basic Principles

### Program Graphs of Structured Programing Constructs

![[Pasted image 20240628171545.png]]

### Examples

![[Pasted image 20240628171652.png]]

![[Pasted image 20240628171713.png]]

![[Pasted image 20240628171733.png]]

![[Pasted image 20240628171759.png]]






---
# *References*
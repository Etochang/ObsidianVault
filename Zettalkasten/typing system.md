202312021749
Meta Tags: #definition 
Tags: [[programming language]] [[computer science]]

# typing system

![[Pasted image 20231202175139.jpg]]
![[Pasted image 20231202175148.jpg]]

A typing system in computer programming is a set of rules and mechanisms that define how different [[data type|data types]] can be used in a [[programming language]]. It governs the ways in which [[variable|variables]], [[expression]], and [[function|functions]] interact with and manipulate data. The main goals of a typing system include:

1. **Type Safety**
	Ensuring [[operation|operations]] are performed on data of the correct [[data type|type]], reducing the likelihood of runtime errors related to type mismatches.
	
1. **Clarity and Readability**
	Making code more understandable by explicitly specifying the types of [[variable|variables]] and [[parameter|parameters]], making the code more self-documenting.
	
1. **Optimization**
	Allowing [[compiler|compilers]]/[[interpreter|interpreters]] to generate efficient [[machine code]] by leveraging knowledge of data types during [[compilation]] or [[interpretation]].
	
1. **Error Detection**
	Catching type-related errors early in the development process, often at [[compile time]], to improve program reliability.
	
1. **Flexibility**
	Providing a balance between strictness and flexibility in handling data types, depending on the language's design philosophy and goals.

## Common Typing Systems

### Static Typing:
- [[variable|Variables]] are [[declaration|explicitly declared]] with their [[data type|types]], and [[type checking]] is performed at [[compile time]].
- **Early error detection** is possible, and the compiled code is often more **efficient**.
### Dynamic Typing:
- [[variable|Variable]] [[data type|types]] are determined at [[runtime]].
- [[type checking|Type checking]] is performed during [[program execution]].
- Allows more flexibility but may lead to runtime errors related to type mismatches.
### Strong Typing:
- Type enforcement is strict, and [[implicit type conversion|implicit type conversions]] are limited.
- [[operation|Operations]] involving different [[data type|types]] may require [[explicit type conversion]].
- Aimed at preventing unintended type-related errors.
### Weak Typing:
- Type enforcement is more relaxed, and [[implicit type conversion|implicit type conversions]] are often performed automatically.
- Allows more flexibility but may lead to unexpected behavior if not carefully managed.
### Duck Typing:
- [[data type|Types]] are determined by the presence of certain [[method|methods]] or properties rather than [[declaration|explicit declarations]].
- "If it looks like a duck, swims like a duck, and quacks like a duck, then it probably is a duck." In programming, if an object behaves like a certain type, it is treated as that type.
### Manifest Typing:
- Type information must be explicitly provided in the code.
- Often associated with statically-typed languages where types are [[declaration|explicitly declared]].
### Inferential Typing (Type Inference):
- Type information is automatically inferred by the [[compiler]] or [[interpreter]] without [[declaration|explicit declarations]].
- Reduces the need for explicit [[type annotation|type annotations]] while maintaining static typing benefits.
### Nominal Typing:
- Types are identified by their names.
- Two types are considered equal if and only if they have the same name or [[declaration|explicit declaration]].
### Structural Typing:
- Types are identified by their structure or shape.
- Two types are considered equal if they have the same structure, regardless of their names.



---
# *References*
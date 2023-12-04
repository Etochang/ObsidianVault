202312022323
Meta Tags: #definition 
Tags: [[computer science]]

# UML class diagram

The [UML](https://en.wikipedia.org/wiki/Unified_Modeling_Language) Class diagram is a graphical notation used to construct and visualize [[OOP|object oriented systems]]. A class diagram in the Unified Modeling Language (UML) is a type of static structure diagram that describes the structure of a system by showing the system's:
- [[class|classes]],
- their [[class#Class Variables|attributes]],
- [[class#Class Methods|operations]],
- and the relationships among objects.

## UML Class Notation

A class represents a concept which encapsulates **state** (attributes/variables) and **behavior** (operations/methods). Each attribute has a [[data type|type]]. Each operation has a [[signature]]. The *class name* is the only ***mandatory information***. 
![[02-class-notation 2.webp]]

---

**Class Name:**
- The name of the class appears in the first partition.

**Class Attributes:**
- Attributes are shown in the second partition.
- The attribute type is shown after the colon.
- Attributes map onto member variables (data members) in code.

**Class Operations (Methods):**
- Operations are shown in the third partition. They are services the class provides.
- The return type of a method is shown after the colon at the end of the method signature.
- The return type of method parameters are shown after the colon following the parameter name. Operations map onto class methods in code

![[03-class-notation-with-examples.webp]]

---

### Class Visibility

![[04-class-attributes-with-different-visibility.webp]]

The +, -, and \# symbols before an attribute and operation name in a class denote the [[visibility]] of the attribute and operation.
- \+ denotes public attributes or operations
- \- denotes private attributes or operations
- \# denotes protected attributes or operations

### Parameter Directionality

![[05-parameter-directionality.webp]]

Each parameter in a an operation (method) may be denoted as **in**, **out**, or **inout**, which specifies its direction with respect to the caller. This directionality is shown before the parameter name.

## Relationships Between Classes

![[07-relationships-between-classes.webp]]

### Inheritance (or Generalization)

![[08-inheritance-in-class-diagram.webp]]

A taxonomic relationship between a more general classifier and a more specific classifier. Each [[instance]] of the specific classifier is also an indirect instance of the general classifier. Thus, the specific classifier inherits the features of the more general classifier.

- **Represents an "is-a" relationship.**
- An abstract class name is shown in italics.
- SubClass1 and SubClass2 are specializations of SuperClass.

### Association

Associations are relationships between classes in a UML Class Diagram. They are represented by a solid line between classes. Associations are typically named using a verb or verb phrase which reflects the real world problem domain.

### Simple Association

![[10-simple-association-example.webp]]

- A structural link between two peer classes.
- **There is an association between Class1 and Class2**

### Cardinality

![[11-associations-with-different-multiplicies.webp]]
Cardinality is expressed in terms of:
- one to one
- one to many
- many to many

### Aggregation

![[12-aggregation.webp]]
A special type of association.
- **It represents a "part of" relationship.**
- **Class2 is part of Class1.**
- Many instances (denoted by the *) of Class2 can be associated with Class1.
- Objects of Class1 and Class2 have separate lifetimes.

### Composition

![[13-composition.webp]]
- A special type of aggregation where parts are destroyed when the whole is destroyed.
- **Objects of Class2 live and die with Class1.**
- Class2 cannot stand by itself.

### Dependency

![[14-dependency.webp]]
An object of one class might use an object of another class in the code of a method. If the object is not stored in any field, then this is modeled as a dependency relationship.

- A special type of association.
- Exists between two classes if changes to the definition of one may cause changes to the other (but not the other way around).
- **Class1 depends on Class2**

The figure below shows an example of dependency. The Person class might have a hasRead method with a Book parameter that returns true if the person has read the book (perhaps by checking some database).
![[15-dependency-example.webp]]




---
# *References*
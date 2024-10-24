202406161735
Meta Tags: #class
Tags: [[software engineering]]

# Documenting Software Analysis

## Complex Object Relationships

- A large software system consists of many objects that are related to each other in various different ways.
- **structural:** share data/methods.
	- Association
	- Aggregation - can exist w/o the child, "has a"
	- Composition - cannot exist without the child, "made up of"
	- Generalization (Inheritance)
- **non-structural:** don't share data/methods, just use the functionality of the other.

![[Pasted image 20240616174242.png]]

## Dependency and Association

- **dependency:** non-structural relationship. One calls/uses the other. 

![[Pasted image 20240616174459.png]]
*online store calls payment module to process payment from customers*

- **association:** one needs to access the other, but doesn't really share any other information. We can use an action verb to explain the relationship.

![[Pasted image 20240616174556.png]]
*online store receives orders and the store needs to process them and access them*

## Aggregation and Composition

- **aggregation:** B cannot exist without being associated with A, but A can exist without B. A contains B. A and B have a "has-a" relationship.

![[Pasted image 20240616174834.png]]
*online store has multiple sales representatives*

- **composition:** B cannot exist without being associated with A, and A cannot exist without B. B is a part of A. A and B have a "whole-to-part" relationship.

![[Pasted image 20240616175024.png]]
*order items must exist to make an order, and an order item must be a part of an order*

1. Establish Entities, Things, Occurrences/Events, Roles, Organizational Units, Places and Structure in the use-cases of the AIB system
2. Focus on identifying objects and establishing relationships among them



---
# *References*
https://canvas.asu.edu/courses/185762/assignments/5104397?module_item_id=13399367
https://canvas.asu.edu/courses/185762/assignments/5104396?module_item_id=13399368

202312040241
Meta Tags: #definition #textbook 
Tags: [[computer science]] [[programming language]] [[Python]]

# Python Sets

`myset = {"apple", "banana", "cherry"}`

Sets are used to store multiple items in a single variable.

Set is one of 4 built-in data types in Python used to store collections of data, the other 3 are [List](https://www.w3schools.com/python/python_lists.asp), [Tuple](https://www.w3schools.com/python/python_tuples.asp), and [Dictionary](https://www.w3schools.com/python/python_dictionaries.asp), all with different qualities and usage.

A set is a collection which is _unordered_, _unchangeable*_, and _unindexed_.

>[!note]
>\*Set _items_ are unchangeable, but you can remove items and add new items.

Sets are written with curly brackets.

>[!example]
>```
>thisset = {"apple", "banana", "cherry"}  
print(thisset)
>```

>[!note]
>Sets are unordered, so you cannot be sure in which order the items will appear.

### Set Items

Set items are **unordered**, **unchangeable**, and **do not allow duplicate values**.
#### Unordered

Unordered means that the items in a set do not have a defined order.

Set items can appear in a different order every time you use them, and cannot be referred to by index or key.
#### Unchangeable

Set items are unchangeable, meaning that we cannot change the items after the set has been created.
>Once a set is created, you cannot change its items, but you can remove items and add new items.
#### Duplicates Not Allowed

Sets cannot have two items with the same value.

>[!example] Duplicate values will be ignored:
>```
>thisset = {"apple", "banana", "cherry", "apple"}  
print(thisset)
>```

>[!note] The values `True` and `1` are considered the same value in sets, and are treated as duplicates:
>```
>thisset = {"apple", "banana", "cherry", True, 1, 2}  
print(thisset)
>```

>[!note] The values `False` and `0` are considered the same value in sets, and are treated as duplicates:
>```
>thisset = {"apple", "banana", "cherry", False, True, 0}  
print(thisset)
>```

### Get the Length of a Set

To determine how many items a set has, use the `len()` function.

>[!example] Get the number of items in a set:
>```
>thisset = {"apple", "banana", "cherry"}  
print(len(thisset))
>```

### Set Data Types

Set items can be of any data type:

>[!example] String, int and boolean data types:
>```
>set1 = {"apple", "banana", "cherry"}  
set2 = {1, 5, 7, 9, 3}  
set3 = {True, False, False}
>```

A set can contain different data types:

>[!example] A set with strings, integers and boolean values:
>```
>set1 = {"abc", 34, True, 40, "male"}
>```

### type()

From Python's perspective, sets are defined as objects with the data type 'set':

`<class 'set'>`

### The set() Constructor

It is also possible to use the set() constructor to make a set.

>[!example] Using the set() constructor to make a set:
>```
>thisset = set(("apple", "banana", "cherry")) 
># note the double round-brackets  
print(thisset)
>```

### Python Collections (Arrays)

See [[Python Lists#Python Collections (Arrays)|here]].

## Accessing Set Items

You cannot access items in a set by referring to an index or a key.

But you can loop through the set items using a `for` loop, or ask if a specified value is present in a set, by using the `in` keyword.

>[!example] Loop through the set, and print the values:
>```
>thisset = {"apple", "banana", "cherry"}  
for x in thisset:  
  print(x)
>```

>[!example] Check if "banana" is present in the set:
>```
>thisset = {"apple", "banana", "cherry"}  
print("banana" in thisset)
>```

### Change Items

>Once a set is created, you cannot change its items, but you can add new items.

## Add Set Items

To add one item to a set use the `add()` method.

>[!example] Add an item to a set, using the `add()` method:
>```
>thisset = {"apple", "banana", "cherry"}  
thisset.add("orange")  
print(thisset)
>```

### Add Sets

To add items from another set into the current set, use the `update()` method.

>[!example] Add elements from `tropical` into `thisset`:
>```
>thisset = {"apple", "banana", "cherry"}  
tropical = {"pineapple", "mango", "papaya"}  
thisset.update(tropical)  
print(thisset)
>```

### Add Any Iterable

The object in the `update()` method does not have to be a set, it can be any iterable object (tuples, lists, dictionaries etc.).

>[!example] Add elements of a list to at set:
>```
>thisset = {"apple", "banana", "cherry"}  
mylist = ["kiwi", "orange"]  
thisset.update(mylist)  
print(thisset)
>```

## Remove Set Items

To remove an item in a set, use the `remove()`, or the `discard()` method.

>[!example] Remove "banana" by using the `remove()` method:
>```
>thisset = {"apple", "banana", "cherry"}  
thisset.remove("banana")  
print(thisset)
>```

>[!note]
>If the item to remove does not exist, `remove()` will raise an error.

>[!example] Remove "banana" by using the `discard()` method:
>```
>thisset = {"apple", "banana", "cherry"}  
thisset.discard("banana")  
print(thisset)
>```

>[!note]
>If the item to remove does not exist, `discard()` will **NOT** raise an error.

You can also use the `pop()` method to remove an item, but this method will remove a random item, so you cannot be sure what item that gets removed.

The return value of the `pop()` method is the removed item.

>[!example] Remove a random item by using the `pop()` method:
>```
>thisset = {"apple", "banana", "cherry"}  
x = thisset.pop()  
print(x)  
print(thisset)
>```

>[!important]
>Sets are _unordered_, so when using the `pop()` method, you do not know which item that gets removed.

>[!example] The `clear()` method empties the set:
>```
>thisset = {"apple", "banana", "cherry"} 
thisset.clear()  
print(thisset)
>```

>[!example] The `del` keyword will delete the set completely:
>```
>thisset = {"apple", "banana", "cherry"}  
del thisset  
print(thisset)
>```

## Loops and Sets

### Loop Items

You can loop through the set items by using a `for` loop:

>[!example] Loop through the set, and print the values:
>```
>thisset = {"apple", "banana", "cherry"}  
for x in thisset:  
  print(x)
>```

## Joining Sets

### Join Two Sets

There are several ways to join two or more sets in Python.

You can use the `union()` method that returns a new set containing all items from both sets, or the `update()` method that inserts all the items from one set into another:

>[!example] The `union()` method returns a new set with all items from both sets:
>```
>set1 = {"a", "b" , "c"}  
set2 = {1, 2, 3}  
set3 = set1.union(set2)  
print(set3)
>```

>[!example] The `update()` method inserts the items in set2 into set1:
>```
>set1 = {"a", "b" , "c"}  
set2 = {1, 2, 3}  
set1.update(set2)  
print(set1)
>```

>[!note]
>Both `union()` and `update()` will exclude any duplicate items.

### Keep ONLY the Duplicates

The `intersection_update()` method will keep only the items that are present in both sets.

>[!example] Keep the items that exist in both set `x`, and set `y`:
>```
>x = {"apple", "banana", "cherry"}  
y = {"google", "microsoft", "apple"}  
x.intersection_update(y)  
print(x)
>```

The `intersection()` method will return a _new_ set, that only contains the items that are present in both sets.

>[!example] Return a set that contains the items that exist in both set `x`, and set `y`:
>```
>x = {"apple", "banana", "cherry"}  
y = {"google", "microsoft", "apple"}  
z = x.intersection(y)  
print(z)
>```

### Keep All, But NOT the Duplicates

The `symmetric_difference_update()` method will keep only the elements that are NOT present in both sets.

>[!example] Keep the items that are not present in both sets:
>```
>x = {"apple", "banana", "cherry"}  
y = {"google", "microsoft", "apple"}  
x.symmetric_difference_update(y)  
print(x)
>```

The `symmetric_difference()` method will return a new set, that contains only the elements that are NOT present in both sets.

>[!example] Return a set that contains all items from both sets, except items that are present in both:
>```
>x = {"apple", "banana", "cherry"}  
y = {"google", "microsoft", "apple"}  
z = x.symmetric_difference(y)  
print(z)
>```

>[!important]
>The values `True` and `1`, as well as `False` and `0`, are considered the same value in sets, and are treated as duplicates.

## Set Methods

|Method|Description|
|---|---|
|[add()](https://www.w3schools.com/python/ref_set_add.asp)|Adds an element to the set|
|[clear()](https://www.w3schools.com/python/ref_set_clear.asp)|Removes all the elements from the set|
|[copy()](https://www.w3schools.com/python/ref_set_copy.asp)|Returns a copy of the set|
|[difference()](https://www.w3schools.com/python/ref_set_difference.asp)|Returns a set containing the difference between two or more sets|
|[difference_update()](https://www.w3schools.com/python/ref_set_difference_update.asp)|Removes the items in this set that are also included in another, specified set|
|[discard()](https://www.w3schools.com/python/ref_set_discard.asp)|Remove the specified item|
|[intersection()](https://www.w3schools.com/python/ref_set_intersection.asp)|Returns a set, that is the intersection of two other sets|
|[intersection_update()](https://www.w3schools.com/python/ref_set_intersection_update.asp)|Removes the items in this set that are not present in other, specified set(s)|
|[isdisjoint()](https://www.w3schools.com/python/ref_set_isdisjoint.asp)|Returns whether two sets have a intersection or not|
|[issubset()](https://www.w3schools.com/python/ref_set_issubset.asp)|Returns whether another set contains this set or not|
|[issuperset()](https://www.w3schools.com/python/ref_set_issuperset.asp)|Returns whether this set contains another set or not|
|[pop()](https://www.w3schools.com/python/ref_set_pop.asp)|Removes an element from the set|
|[remove()](https://www.w3schools.com/python/ref_set_remove.asp)|Removes the specified element|
|[symmetric_difference()](https://www.w3schools.com/python/ref_set_symmetric_difference.asp)|Returns a set with the symmetric differences of two sets|
|[symmetric_difference_update()](https://www.w3schools.com/python/ref_set_symmetric_difference_update.asp)|inserts the symmetric differences from this set and another|
|[union()](https://www.w3schools.com/python/ref_set_union.asp)|Return a set containing the union of sets|
|[update()](https://www.w3schools.com/python/ref_set_update.asp)|Update the set with the union of this set and others|

# [[Python Dictionaries]]

---
# *References*
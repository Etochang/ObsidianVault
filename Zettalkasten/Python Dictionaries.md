202312040308
Meta Tags: #definition #textbook 
Tags: [[computer science]] [[programming language]] [[Python]]

# Python Dictionaries

- [[#Dictionaries|Dictionaries]]
	- [[#Dictionaries#Dictionary Items|Dictionary Items]]
		- [[#Dictionary Items#Ordered or Unordered?|Ordered or Unordered?]]
		- [[#Dictionary Items#Changeable|Changeable]]
		- [[#Dictionary Items#Duplicates Not Allowed|Duplicates Not Allowed]]
	- [[#Dictionaries#Dictionary Length|Dictionary Length]]
	- [[#Dictionaries#Dictionary Data Types|Dictionary Data Types]]
	- [[#Dictionaries#type()|type()]]
	- [[#Dictionaries#The dict() Constructor|The dict() Constructor]]
	- [[#Dictionaries#Python Collections (Arrays)|Python Collections (Arrays)]]
- [[#Accessing Dictionary Items|Accessing Dictionary Items]]
	- [[#Accessing Dictionary Items#Get Keys|Get Keys]]
	- [[#Accessing Dictionary Items#Get Values|Get Values]]
	- [[#Accessing Dictionary Items#Get Items|Get Items]]
	- [[#Accessing Dictionary Items#Check if Key Exists|Check if Key Exists]]
- [[#Change Items|Change Items]]
	- [[#Change Items#Update Dictionary|Update Dictionary]]
- [[#Adding Dictionary Items|Adding Dictionary Items]]
	- [[#Adding Dictionary Items#Update Dictionary|Update Dictionary]]
- [[#Removing Items|Removing Items]]
- [[#Loops and Dictionaries|Loops and Dictionaries]]
- [[#Copying Dictionaries|Copying Dictionaries]]
- [[#Nested Dictionaries|Nested Dictionaries]]
	- [[#Nested Dictionaries#Access Items in Nested Dictionaries|Access Items in Nested Dictionaries]]
- [[#Dictionary Methods|Dictionary Methods]]



## Dictionaries

```
thisdict = {  
  "brand": "Ford",  
  "model": "Mustang",  
  "year": 1964  
}
```

Dictionaries are used to store data values in key:value pairs.

A dictionary is a collection which is ordered\*, changeable and do not allow duplicates.

>As of Python version 3.7, dictionaries are _ordered_. In Python 3.6 and earlier, dictionaries are _unordered_.

Dictionaries are written with curly brackets, and have keys and values:

>[!example] Create and print a dictionary:
>```
>thisdict = {  
  "brand": "Ford",  
  "model": "Mustang",  
  "year": 1964  
}  
print(thisdict)
>```

### Dictionary Items

Dictionary items are **ordered**, **changeable**, and **do not allow duplicates**.

Dictionary items are presented in key:value pairs, and can be referred to by using the key name.

>[!example] Print the "brand" value of the dictionary:
>```
>thisdict = {  
  "brand": "Ford",  
  "model": "Mustang",  
  "year": 1964  
}  
print(thisdict["brand"])
>```


#### Ordered or Unordered?

When we say that dictionaries are ordered, it means that the items have a defined order, and that order will not change.

Unordered means that the items do not have a defined order, you cannot refer to an item by using an index.

#### Changeable

Dictionaries are changeable, meaning that we can change, add or remove items after the dictionary has been created.
#### Duplicates Not Allowed

Dictionaries cannot have two items with the same key:

>[!example] Duplicate values will overwrite existing values:
>```
>thisdict = {  
  "brand": "Ford",  
  "model": "Mustang",  
  "year": 1964,  
  "year": 2020  
}  
print(thisdict)
>```

### Dictionary Length

To determine how many items a dictionary has, use the `len()` function:

>[!example] Print the number of items in the dictionary:
>```
>print(len(thisdict))
>```

### Dictionary Data Types

The keys and values in dictionary items can be of any data type:

>[!example] String, int, boolean, and list data types:
>```
>thisdict = {  
  "brand": "Ford",  
  "electric": False,  
  "year": 1964,  
  "colors": ["red", "white", "blue"]  
}
>```

### type()

From Python's perspective, dictionaries are defined as objects with the data type 'dict':

`<class 'dict'>`

### The dict() Constructor

It is also possible to use the dict() constructor to make a dictionary.

>[!example] Using the dict() method to make a dictionary:
>```
>thisdict = dict(name = "John", age = 36, country = "Norway")  
print(thisdict)
>```

### Python Collections (Arrays)

See [[Python Lists#Python Collections (Arrays)|here]].

## Accessing Dictionary Items

You can access the items of a dictionary by referring to its key name, inside square brackets:

>[!example] Get the value of the "model" key:
>```
>  "brand": "Ford",  
  "model": "Mustang",  
  "year": 1964  
}  
x = thisdict["model"]
>```

There is also a method called `get()` that will give you the same result:

>[!example] Get the value of the "model" key:
>```
>x = thisdict.get("model")
>```

### Get Keys

The `keys()` method will return a list of all the keys in the dictionary.

>[!example] Get a list of the keys:
>```
>x = thisdict.keys()
>```

The list of the keys is a _view_ of the dictionary, meaning that any changes done to the dictionary will be reflected in the keys list.

>[!example] Add a new item to the original dictionary, and see that the keys list gets updated as well:
>```
>car = {  
"brand": "Ford",  
"model": "Mustang",  
"year": 1964  
}  
x = car.keys()  
print(x) #before the change  
car["color"] = "white"  
print(x) #after the change
>```

### Get Values

The `values()` method will return a list of all the values in the dictionary.

>[!example] Get a list of the values:
>```
>x = thisdict.values()
>```

The list of the values is a _view_ of the dictionary, meaning that any changes done to the dictionary will be reflected in the values list.

>[!example] Make a change in the original dictionary, and see that the values list gets updated as well:
>```
>car = {  
"brand": "Ford",  
"model": "Mustang",  
"year": 1964  
}  
x = car.values()  
print(x) #before the change  
car["year"] = 2020  
print(x) #after the change
>```

>[!example] Add a new item to the original dictionary, and see that the values list gets updated as well:
>```
>car = {  
"brand": "Ford",  
"model": "Mustang",  
"year": 1964  
}  
x = car.values()  
print(x) #before the change  
car["color"] = "red"  
print(x) #after the change
>```

### Get Items

The `items()` method will return each item in a dictionary, as tuples in a list.

>[!example] Get a list of the key:value pairs in tuples
>```
>x = thisdict.items()
>```

The returned list is a _view_ of the items of the dictionary, meaning that any changes done to the dictionary will be reflected in the items list.

>[!example] Make a change in the original dictionary, and see that the items list gets updated as well:
>```
>car = {  
"brand": "Ford",  
"model": "Mustang",  
"year": 1964  
}  
x = car.items()  
print(x) #before the change 
car["year"] = 2020  
print(x) #after the change
>```

>[!example] Add a new item to the original dictionary, and see that the items list gets updated as well:
>```
>car = {  
"brand": "Ford",  
"model": "Mustang",  
"year": 1964  
}  
x = car.items()  
print(x) #before the change  
car["color"] = "red"  
print(x) #after the change
>```

### Check if Key Exists

To determine if a specified key is present in a dictionary use the `in` keyword:

>[!example] Check if "model" is present in the dictionary:
>```
>thisdict = {  
  "brand": "Ford",  
  "model": "Mustang",  
  "year": 1964  
}  
if "model" in thisdict:  
  print("Yes, 'model' is one of the keys in the thisdict dictionary")
>```

## Change Items

You can change the value of a specific item by referring to its key name:

>[!example] Change the "year" to 2018:
>```
>thisdict = {  
  "brand": "Ford",  
  "model": "Mustang",  
  "year": 1964  
}  
thisdict["year"] = 2018
>```

### Update Dictionary

The `update()` method will update the dictionary with the items from the given argument.

The argument must be a dictionary, or an iterable object with key:value pairs.

>[!example] Update the "year" of the car by using the `update()` method:
>```
>thisdict = {  
  "brand": "Ford",  
  "model": "Mustang",  
  "year": 1964  
}  
thisdict.update({"year": 2020})
>```

## Adding Dictionary Items

Adding an item to the dictionary is done by using a new index key and assigning a value to it:

>[!example]
>```
>thisdict = {  
  "brand": "Ford",  
  "model": "Mustang",  
  "year": 1964  
}  
thisdict["color"] = "red"  
print(thisdict)
>```

### Update Dictionary

The `update()` method will update the dictionary with the items from a given argument. If the item does not exist, the item will be added.

The argument must be a dictionary, or an iterable object with key:value pairs.

>[!example] Add a color item to the dictionary by using the `update()` method:
>```
>thisdict = {  
  "brand": "Ford",  
  "model": "Mustang",  
  "year": 1964  
}  
thisdict.update({"color": "red"})
>```

## Removing Items

There are several methods to remove items from a dictionary:

>[!example] The `pop()` method removes the item with the specified key name:
>```
>thisdict = {  
  "brand": "Ford",  
  "model": "Mustang",  
  "year": 1964  
}  
thisdict.pop("model")  
print(thisdict)
>```

>[!example] The `popitem()` method removes the last inserted item (in versions before 3.7, a random item is removed instead):
>```
>thisdict = {  
  "brand": "Ford",  
  "model": "Mustang",  
  "year": 1964  
}  
thisdict.popitem()  
print(thisdict)
>```

>[!example] The `del` keyword removes the item with the specified key name:
>```
>thisdict = {  
  "brand": "Ford",  
  "model": "Mustang",  
  "year": 1964  
}  
del thisdict["model"]  
print(thisdict)
>```

>[!error] The `del` keyword can also delete the dictionary completely:
>```
>thisdict = {  
  "brand": "Ford",  
  "model": "Mustang",  
  "year": 1964  
}  
del thisdict  
print(thisdict) #this will cause an error because "thisdict" no longer exists.
>```

>[!example] The `clear()` method empties the dictionary:
>```
>thisdict = {  
  "brand": "Ford",  
  "model": "Mustang",  
  "year": 1964  
}  
thisdict.clear()  
print(thisdict)
>```

## Loops and Dictionaries

You can loop through a dictionary by using a `for` loop.

When looping through a dictionary, the return value are the *keys* of the dictionary, but there are methods to return the _values_ as well.

>[!example] Print all key names in the dictionary, one by one:
>```
>for x in thisdict:  
  print(x)
>```

>[!example] Print all _values_ in the dictionary, one by one:
>```
>for x in thisdict:  
  print(thisdict[x])
>```

>[!example] You can use the `keys()` method to return the keys of a dictionary:
>```
>for x in thisdict.keys():  
  print(x)
>```

>[!example] Loop through both _keys_ and _values_, by using the `items()` method:
>```
>for x, y in thisdict.items():  
  print(x, y)
>```

## Copying Dictionaries

You cannot copy a dictionary simply by typing `dict2 = dict1`, because: `dict2` will only be a _reference_ to `dict1`, and changes made in `dict1` will automatically also be made in `dict2`.

There are ways to make a copy, one way is to use the built-in Dictionary method `copy()`.

>[!example] Make a copy of a dictionary with the `copy()` method:
>```
>thisdict = {  
  "brand": "Ford",  
  "model": "Mustang",  
  "year": 1964  
}  
mydict = thisdict.copy()  
print(mydict)
>```

Another way to make a copy is to use the built-in function `dict()`.

>[!example] Make a copy of a dictionary with the `dict()` function:
>```
>thisdict = {  
  "brand": "Ford",  
  "model": "Mustang",  
  "year": 1964  
}  
mydict = dict(thisdict)  
print(mydict)
>```

## Nested Dictionaries

A dictionary can contain dictionaries, this is called nested dictionaries.

>[!example] Create a dictionary that contain three dictionaries:
>```
>myfamily = {  
  "child1" : {  
    "name" : "Emil",  
    "year" : 2004  
  },  
  "child2" : {  
    "name" : "Tobias",  
    "year" : 2007  
  },  
  "child3" : {  
    "name" : "Linus",  
    "year" : 2011  
  }  
}
>```

Or, if you want to add three dictionaries into a new dictionary:

>[!example] Create three dictionaries, then create one dictionary that will contain the other three dictionaries:
>```
>child1 = {  
  "name" : "Emil",  
  "year" : 2004  
}  
child2 = {  
  "name" : "Tobias",  
  "year" : 2007  
}  
child3 = {  
  "name" : "Linus",  
  "year" : 2011  
}  
myfamily = {  
  "child1" : child1,  
  "child2" : child2,  
  "child3" : child3  
}
>```

### Access Items in Nested Dictionaries

To access items from a nested dictionary, you use the name of the dictionaries, starting with the outer dictionary:

>[!example] Print the name of child 2:
>```
>print(myfamily["child2"]["name"])
>```

## Dictionary Methods

|Method|Description|
|---|---|
|[clear()](https://www.w3schools.com/python/ref_dictionary_clear.asp)|Removes all the elements from the dictionary|
|[copy()](https://www.w3schools.com/python/ref_dictionary_copy.asp)|Returns a copy of the dictionary|
|[fromkeys()](https://www.w3schools.com/python/ref_dictionary_fromkeys.asp)|Returns a dictionary with the specified keys and value|
|[get()](https://www.w3schools.com/python/ref_dictionary_get.asp)|Returns the value of the specified key|
|[items()](https://www.w3schools.com/python/ref_dictionary_items.asp)|Returns a list containing a tuple for each key value pair|
|[keys()](https://www.w3schools.com/python/ref_dictionary_keys.asp)|Returns a list containing the dictionary's keys|
|[pop()](https://www.w3schools.com/python/ref_dictionary_pop.asp)|Removes the element with the specified key|
|[popitem()](https://www.w3schools.com/python/ref_dictionary_popitem.asp)|Removes the last inserted key-value pair|
|[setdefault()](https://www.w3schools.com/python/ref_dictionary_setdefault.asp)|Returns the value of the specified key. If the key does not exist: insert the key, with the specified value|
|[update()](https://www.w3schools.com/python/ref_dictionary_update.asp)|Updates the dictionary with the specified key-value pairs|
|[values()](https://www.w3schools.com/python/ref_dictionary_values.asp)|Returns a list of all the values in the dictionary|

# [[Python If ... Else]]


---
# *References*
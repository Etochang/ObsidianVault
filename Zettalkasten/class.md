202310231633
Meta Tags: #MOC  
Tags [[computer science]] [[OOP]]

# class

## [[C++]]

```ad-example
title: Car Analogy
Everything in C++ is associated with classes and objects, along with its attributes and methods. A car is an object. It has attributes, like color and weight, as well as methods, like drive and brake.

**Attributes** and **methods** are basically variables and functions that belong to the class. As such, they are referred to as **class members**.
```
### Creating a Class

```
class MyClass {          //The class
	public:              //access specifier
		int myNum;       //attribute (int)
		string MyString; //attribute (string)
};
```
```ad-info
title: Example Explained
- The `class` keyword is used to create a class called `MyClass`.
- The `public` keyword is an **access specifier**, which specifies that members of the class are accessible from outside the class.
- Inside the class, there is an integer variable `myNum` and a string variable `myString`. When variables are declared within a class, they are called **attributes**.
- At last, end the class definition with a **semicolon** `;`.

```

### Class Variables

AKA member variables or attributes, they refer to variables that are declared within a class. Usually put into `private` for encapsulation purposes. Static member variables are shared across all instances, while regular ones are unique per instance.

### Class Methods

Methods are [[C++ Functions|functions]] that belong to the class. AKA member functions or [[operation|operations]], and are usually present in the `public` section of a class due to being the interface.

There are two ways to define functions that belong to a class:
- Inside class definition
- Outside class definition

Inside class definition example:

```
class MyClass {        // The class  
  public:              // Access specifier  
    void myMethod() {  // Method/function defined inside
      cout << "Hello World!";  
    }  
};  
  
int main() {  
  MyClass myObj;     // Create an object of MyClass  
  myObj.myMethod();  // Call the method  
  return 0;  
}
```

To define a function outside the class definition, you have to declare it inside the class and then define it outside. This is done by specifying the name of the class, followed by the `::` operator, followed by the name of the function:

```
class MyClass {        // The class  
  public:              // Access specifier  
    void myMethod();   // Method/function declaration  
};  
  
// Method/function definition outside the class  
void MyClass::myMethod() {  
  cout << "Hello World!";  
}  
  
int main() {  
  MyClass myObj;     // Create an object of MyClass  
  myObj.myMethod();  // Call the method  
  return 0;  
}
```

### Constructors

A constructor in C++ is a **special method** that is automatically called when an object of a class is created. To create a constructor, use the same name as the class, followed by parentheses:

```
class MyClass {     // The class  
  public:           // Access specifier  
    MyClass() {     // Constructor  
      cout << "Hello World!";  
    }  
};
```

```ad-note
The constructor has the same name as the class, it is always `public`, and it does not have any return value.
```

#### Constructor Parameters

Constructors can also take parameters, which can be useful for setting initial values for attributes.

```
class MyClass {     // The class  
  public:           // Access specifier  
    MyClass(int num, string str) {     // Constructor  
      cout << "Hello World!";  
      age = num;
      name = str;
    }  
  private:
    int age;
    string name;
};
```

They can also be defined out of the class, just like regular [[C++ Functions|functions]].

```
class MyClass {     // The class  
  public:           // Access specifier  
    MyClass();      // declared constructor
};

MyClass::MyClass() {
	cout << "Hello World!";
}
```

```ad-info
Constructors in C++ do not have a return type, even `void`.

```

There is also a shorthand for writing constructors:

```
class MyClass {     // The class  
  public:           // Access specifier  
    MyClass(int num, string str) : age(num), name(str)
    {  
      cout << "Hello World!";  
    }  
  private:
    int age;
    string name;
};
```

### Access Specifiers

```
class MyClass {  // The class  
  public:        // Access specifier  
    // class members goes here  
};
```

In this example, `public` is an **access specifier**. They define how the members (attributes and methods) of a class can be accessed. 

In C++, there are three access specifier:
- `public` - members are accessible from outside the class; identifies the interface portion of the class.
- `private` - members cannot be accessed (or viewed) from outside the class; identifies the implementation portion of the class.
- `protected` - members cannot be accessed from outside the class, however, they can be accessed in inherited classes. 

```ad-note
It is possible to access private members of a class using a public method inside the same class. See [[class#Encapsulation|encapsulation]].
```
```ad-tip
It is considered good practice to declare your class attributes as private (as often as you can). This will reduce the possibility of yourself (or others) to mess up the code.
```

By default, all members of a class are `private` if you don't specify an access specifier:

```
class MyClass {  
  int x;   // Private attribute  
  int y;   // Private attribute  
};
```

### Encapsulation

The meaning of encapsulation is the make sure that "sensitive" data is hidden from users. 

#### Access Private Members

Use public "get" and "set" methods:

```
#include <iostream>  
using namespace std;  
  
class Employee {  
  private:  
    // Private attribute  
    int salary;  
  
  public:  
    // Setter  
    void setSalary(int s) {  
      salary = s;  
    }  
    // Getter  
    int getSalary() {  
      return salary;  
    }  
};  
  
int main() {  
  Employee myObj;  
  myObj.setSalary(50000);  
  cout << myObj.getSalary();  
  return 0;  
}
```

### Inheritance

In C++, it is possible to inherit attributes and methods from one class to another. This concept has two categories:
- **derived class** (child) - the class that inherits
- **base class** (parent) - the class being inherited from

To inherit from a class, use the `:` symbol.

```
// Base class  
class Vehicle {  
  public:  
    string brand = "Ford";  
    void honk() {  
      cout << "Tuut, tuut! \n" ;  
    }  
};  
  
// Derived class  
class Car: public Vehicle {  
  public:  
    string model = "Mustang";  
};  
  
int main() {  
  Car myCar;  
  myCar.honk();  
  cout << myCar.brand + " " + myCar.model;  
  return 0;  
}
```

#### Multilevel Inheritance

```
// Base class (parent)  
class MyClass {  
  public:  
    void myFunction() {  
      cout << "Some content in parent class." ;  
    }  
};  
  
// Derived class (child)  
class MyChild: public MyClass {  
};  
  
// Derived class (grandchild)  
class MyGrandChild: public MyChild {  
};
```

#### Multiple Inheritance

A class can be derived from more than one base class, using a comma-separated list:

```
// Base class  
class MyClass {  
  public:  
    void myFunction() {  
      cout << "Some content in parent class." ;  
    }  
};  
  
// Another base class  
class MyOtherClass {  
  public:  
    void myOtherFunction() {  
      cout << "Some content in another class." ;  
    }  
};  
  
// Derived class  
class MyChildClass: public MyClass, public MyOtherClass {  
};
```

#### Access Specifiers - Inheritance

Here you can see that there is an access specifier before the inheritance:
`class MyChildClass: public MyClass {};`
- `public` - public -> public, protected -> protected, private -> private
- `protected` - public -> protected, protected -> protected, private -> private
- `private` - public -> private, protected -> private, private -> private

### Polymorphism

Polymorphism means "many forms", and it occurs when we have many classes that are related to each other by inheritance.

For example, think of a base class called `Animal` that has a method called `animalSound()`. Derived classes of Animals could be Pigs, Cats, Dogs, Birds - And they also have their own implementation of an animal sound (the pig oinks, and the cat meows, etc.):

```
// Base class  
class Animal {  
  public:  
    void animalSound() {  
      cout << "The animal makes a sound \n";  
    }  
};  
  
// Derived class  
class Pig : public Animal {  
  public:  
    void animalSound() {  
      cout << "The pig says: wee wee \n";  
    }  
};  
  
// Derived class  
class Dog : public Animal {  
  public:  
    void animalSound() {  
      cout << "The dog says: bow wow \n";  
    }  
};
```

---
# *References*

[C++ OOP (Object-Oriented Programming) (w3schools.com)](https://www.w3schools.com/cpp/cpp_oop.asp)
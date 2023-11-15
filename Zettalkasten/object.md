202311041459
Meta Tags: #definition 
Tags: [[computer science]] [[OOP]]

# object

## [[C++]]

In C++, an object is created from a [[class#C++|class]]. Let's say we have a class `MyClass`:
```
class MyClass {       // The class  
  public:             // Access specifier  
    int myNum;        // Attribute (int variable)  
    string myString;  // Attribute (string variable)  
};
```

To create an object of `MyClass`, specify the class name, followed by the object name. To access the class attributes (`myNum` and `myString`), use the `.` syntax of the object:

```
int main() {  
  MyClass myObj;  // Create an object of MyClass  
  
  // Access attributes and set values  
  myObj.myNum = 15;   
  myObj.myString = "Some text";  
  
  // Print attribute values  
  cout << myObj.myNum << "\n";  
  cout << myObj.myString;  
  return 0;  
}
```

---
# *References*
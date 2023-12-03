202312022048
Meta Tags: #question
Tags: [[C++]] [[programming language]] [[computer science]]

# When can C++ code compile but result in a runtime error❔

1. **Dereferencing a null pointer:**
    
    `int* ptr = nullptr; *ptr = 5; // Compiles but leads to a runtime error (undefined behavior)`
    
    >Dereferencing a null pointer or an uninitialized pointer can lead to undefined behavior and a runtime error.
    
2. **Array out-of-bounds access:**
    
    `int arr[5] = {1, 2, 3, 4, 5}; int value = arr[10]; // Compiles but results in a runtime error (out-of-bounds access)`
    
    >Accessing elements beyond the bounds of an array can cause runtime errors and lead to undefined behavior.
    
3. **Dividing by zero:**
    
    `int a = 5; int b = 0; int result = a / b; // Compiles but results in a runtime error (division by zero)`
    
   > Dividing by zero is undefined behavior in C++, and it typically results in a runtime error.
    
4. **Using an uninitialized variable:**
    
    `int x; int y = x + 5; // Compiles but results in a runtime error (using uninitialized variable)`
    
    >Accessing the value of an uninitialized variable can lead to unpredictable behavior and runtime errors.
    
5. **Dynamic memory issues:**
    
    `int* arr = new int[5]; delete[] arr; arr[0] = 10; // Compiles but results in a runtime error (using deleted memory)`
    
    >Accessing memory that has been freed or deleted can result in runtime errors.




---
# *References*
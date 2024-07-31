#  `<string>` Header

The `<string>` header in C++ is part of the Standard Library and provides the definition for the `std::string` class, which is a versatile way to handle sequences of characters (strings). 

Unlike C-style strings (`char` arrays), `std::string` provides various member functions and operators to manipulate strings conveniently and safely.

<br/>

1. **Safety**: `std::string` handles memory management automatically, reducing the risk of memory leaks and buffer overflows.
2. **Functionality**: `std::string` includes a wide range of built-in functions for common operations like concatenation, comparison, substring extraction, etc.
3. **Flexibility**: It can be easily resized and modified, unlike fixed-size C-style strings.

<br/>

```cpp
#include <string>
```



<br/>

## Basic Usage

1. **Declaration and Initialization**:

   ```cpp
   std::string str1; // Default constructor, empty string
   std::string str2 = "Hello, World!"; // Initialization with a string literal
   std::string str3("Hello, World!"); // Another way to initialize
   std::string str4(str3); // Copy constructor
   ```

2. **Concatenation**:

   ```cpp
   std::string str5 = str2 + " How are you?";
   ```

3. **Accessing Characters**:
   ```cpp
   char ch = str2[1]; // Access the second character
   ```

4. **Length of the String**:
   ```cpp
   size_t len = str2.length(); // Get the length of the string
   ```

5. **Substring**:
   ```cpp
   std::string substr = str2.substr(7, 5); // Get substring starting at index 7 with length 5
   ```

6. **Comparison**:
   ```cpp
   if (str2 == "Hello, World!") {
       // Strings are equal
   }
   ```

7. **Searching**:
   ```cpp
   size_t pos = str2.find("World"); // Find the substring "World"
   if (pos != std::string::npos) {
       // Substring found
   }
   ```

8. **String to Int (stoi)**

   ```cpp
   string str1 = "123";
   string str2 = "456xyz";
       
   int num1 = std::stoi(str1); // Converts the whole string to an integer
   size_t pos;
   int num2 = std::stoi(str2, &pos); // Converts part of the string up to the first non-numeric character
   ```

9. **Case Conversion**:

   ```cpp
   // Convert to uppercase
   for (char &c : str2) {
       c = std::toupper(c);
   }
   
   // Convert to lowercase
   for (char &c : str2) {
       c = std::tolower(c);
   }
   ```
# Standard Library

> A collection of pre-written classes, functions, and types that are provided by the programming language. 
> These libraries are designed to provide commonly needed functionality, making it easier for developers to write efficient and error-free code without having to reinvent the wheel. 



<br/>

## Core Components

- **Containers**: These are data structures like `std::vector`, `std::list`, `std::map`, and `std::set`, which provide ways to store and manage collections of objects.
- **Algorithms**: Functions for performing operations on containers, such as sorting, searching, and transforming data. Examples include `std::sort`, `std::find`, and `std::accumulate`.
- **Iterators**: Objects that enable traversal of containers. They provide a way to access elements of a container sequentially without exposing the underlying structure.
- **Streams**: Classes for input and output operations, such as `std::cin` for standard input, `std::cout` for standard output, and `std::ifstream`/`std::ofstream` for file operations.
- **Strings**: The `std::string` class and related functions for managing sequences of characters.
- **Utilities**: General-purpose utilities such as `std::pair`, `std::tuple`, and `std::optional`.

<br/>

## STD

`std` is the standard namespace used by the C++ Standard Library. Namespaces are used in C++ to organize code and to prevent name collisions. 

1. **Namespace**: `std` is a namespace that contains all the C++ Standard Library entities. By placing these entities in a namespace, it helps avoid naming conflicts that might occur if the same names are used in different parts of a program or in different libraries.

2. **Usage**: 

   ```cpp
   #include <iostream>
   #include <string>
   
   int main() {
       std::string greeting = "Hello, World!";
       std::cout << greeting << std::endl;
       return 0;
   }
   ```

3. **Using `using` Directive**: To avoid having to prefix everything with `std::`, you can use the `using` directive.

   > this is generally not recommended for larger projects or headers to avoid naming conflicts

   ```cpp
   #include <iostream>
   #include <string>
   
   using namespace std;
   
   int main() {
       string greeting = "Hello, World!";
       cout << greeting << endl;
       return 0;
   }
   ```

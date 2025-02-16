# String Types in C++

## 1. std::string

- Modern C++ string class from Standard Template Library
- **Dynamic** size, **automatic** memory management
- Part of `<string>` header

```cpp
#include <string>
std::string str = "hello";
str += " world"; // automatic resizing
```

<img src="https://julien.jorge.st/posts/en/effortless-performance-improvements-in-cpp-std-string_view/images/string_view-example.png" alt="st" style="zoom:30%;" />

<br/>

## 2. const char*

- **Pointer** to constant character array
- Cannot modify pointed string content
- Often used for *string literals*

```cpp
const char* str = "hello"; // string literal
// str[0] = 'H'; // error: read-only memory
```

<br/>

## 3. char*

- **Mutable pointer** to character array
- Can modify both pointer and content
- Manual memory management required

```cpp
char* str = new char[6];
strcpy(str, "hello");
str[0] = 'H'; // ok
delete[] str; // manual cleanup needed
```

<br/>

## 4. Key Differences

**Memory Management:**
- `string`: automatic
- `const char*`: typically static/read-only
- `char*`: manual allocation/deallocation

**Size Modification:**
- `string`: dynamic
- `const char*`: fixed
- `char*`: fixed unless reallocated

**Safety Level:**
- `string`: highest (bounds checking)
- `const char*`: medium (prevents content modification)
- `char*`: lowest (no built-in safety)



<br/>

## 5. Common Operations

```cpp
// string operations
string str1 = "hello";
string str2 = " world";
string combined = str1 + str2;       // concatenation
bool contains = str1.find('e') != string::npos;  // searching
str1[0] = 'H';                       // character modification
string slice = str1.substr(1, 3);    // "ell"

// const char* operations
const char* text1 = "hello";
const char* text2 = "world";
int compare = strcmp(text1, text2);   // string comparison
const char* found = strchr(text1, 'l'); // find first occurrence
size_t len = strlen(text1);           // length
bool equal = (strcmp(text1, "hello") == 0); // equality check

// char* operations
char buffer[50];
strcpy(buffer, "hello");              // copy string
strcat(buffer, " world");            // append
strncat(buffer, "!!!", 3);           // append with length limit
char* token = strtok(buffer, " ");   // tokenize string

// conversion between types
string cpp_str = "test";
const char* c_str = cpp_str.c_str(); // string to const char*

char mutable_str[] = "hello";
string cpp_str2(mutable_str);        // char* to string

// string formatting
char formatted[100];
sprintf(formatted, "Count: %d", 42);  // C-style formatting

// string manipulation
char text[] = "Hello World";
strupr(text);                        // to upper case (Windows)
strlwr(text);                        // to lower case (Windows)
strrev(text);                        // reverse string (Windows)

// memory-safe copying
char dest[10];
strncpy(dest, "too long string", 9); // copy with length limit
dest[9] = '\0';                      // null terminate manually
```









<br/><br/>

참고

https://julien.jorge.st/posts/en/effortless-performance-improvements-in-cpp-std-string_view/

https://noel-embedded.tistory.com/1171
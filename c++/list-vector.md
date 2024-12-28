# List

-  **STL Container** that stores elements randomly in unrelated locations
-  Doubly-linked list, so each element knows its previous and next elements
- The order is preserved even when elements are inserted or removed from the middle of the list

<img src="https://github.com/silverpoodle/typora-images/blob/main/image-20240813141253098.png?raw=true" alt="image" style="zoom:80%;" />

<br/><br/>

### 1. Insertion:

- `push_back(value)`: Adds an element to the end of the list.

- `push_front(value)`: Adds an element to the beginning of the list.

- `insert(iterator, value)`: Inserts an element at a specific position.

  <br/>

### 2. Deletion:

- `pop_back()`: Removes the last element.

- `pop_front()`: Removes the first element.

- `remove(value)`: Removes all elements with the specified value.

- `remove_if(predicate)`: Removes elements that satisfy a condition.

  <br/>

### 3. Accessing elements:

- `front()`: Returns a reference to the first element.

- `back()`: Returns a reference to the last element.

  <br/>

### 4. Iterating:

- You can use range-based for loops or iterators to traverse the list.

  <br/>

### 5. Size operations:

- `size()`: Returns the number of elements in the list.

  <br/>

### 6. Clearing:

- `clear()`: Removes all elements from the list.

  <br/>



<br/>

```c++
#include <iostream>
#include <list>

int main() {
    std::list<int> myList;

    // 1. Insertion
    // Insert at the back
    myList.push_back(10);
    myList.push_back(20);

    // Insert at the front
    myList.push_front(5);

    // Insert at a specific position
    auto it = myList.begin();
    std::advance(it, 2);  // Move the iterator forward by 2 positions
    myList.insert(it, 15);

    // 2. Deletion
    // Remove from the back
    myList.pop_back();

    // Remove from the front
    myList.pop_front();

    // Remove a specific element
    myList.remove(15);

    // Remove elements that satisfy a condition
    myList.remove_if([](int n) { return n % 2 == 0; });

    // 3. Accessing elements
    std::cout << "First element: " << myList.front() << std::endl;
    std::cout << "Last element: " << myList.back() << std::endl;

    // 4. Iterating through the list
    std::cout << "List contents: ";
    for (const auto& elem : myList) {
        std::cout << elem << " ";
    }
    std::cout << std::endl;

    // 5. Size operations
    std::cout << "List size: " << myList.size() << std::endl;

    // 6. Clearing the list
    myList.clear();

    return 0;
}
```

<br/>



> When to use List:
>
> 1. When you need frequent insertions or deletions in the middle of the container.
> 2. When you don't need random access to elements.
> 3. When you want iterators to remain valid after insertions or deletions.

<br/><br/>

# Vector

- Vectors are used to store elements of similar data types
- Unlike Arrays, the size of a vector can grow dynamically

<br/>

<img src="https://miro.medium.com/v2/resize:fit:827/1*8I2Y2w4uPyJ7GHVjq4wkVw.png" alt="image" style="zoom:80%;" />



<br/><br/>

### 1. Insertion:

- `push_back(value)`: Adds an element to the end of the vector.

- `insert(iterator, value)`: Inserts an element at a specific position.

- No direct `push_front()` method;  use `insert(vector.begin(), value)` instead.

  <br/>

### 2. Deletion:

- `pop_back()`: Removes the last element.
- `erase(iterator)`: Removes the element at the specified position.
- `erase(iterator_begin, iterator_end)`: Removes elements in the range [begin, end).
- To remove specific values, use the erase-remove idiom:
  -  `vector.erase(std::remove(vector.begin(), vector.end(), value), vector.end())`
- For conditional removal, use:
  -  `vector.erase(std::remove_if(vector.begin(), vector.end(), predicate), vector.end())`

<br/>

### 3. Accessing elements:

- `front()`: Returns a reference to the first element.
- `back()`: Returns a reference to the last element.
- `operator[]`: Accesses element at specified index (e.g., `vector[i]`).
- `at(index)`: Accesses element at specified index with bounds checking.

<br/>

### 4. Iterating:

- You can use range-based for loops or iterators to traverse the list.

  <br/>

### 5. Size operations:

- `size()`: Returns the number of elements in the vector.

- `capacity()`: Returns the current capacity of the vector.

- `reserve(n)`: Reserves space for at least n elements.

- `resize(n)`: Changes the size of the vector to n elements.

  <br/>

### 6. Clearing:

- `clear()`: Removes all elements from the list.

  <br/><br/>

```c++
#include <iostream>
#include <vector>

int main() {
    std::vector<int> myVector;

    // 1. Insertion
    // Insert at the back
    myVector.push_back(10);
    myVector.push_back(20);

    // Insert at the front (less efficient for vector)
    myVector.insert(myVector.begin(), 5);

    // Insert at a specific position
    auto it = myVector.begin();
    std::advance(it, 2);  // Move the iterator forward by 2 positions
    myVector.insert(it, 15);

    // 2. Deletion
    // Remove from the back
    myVector.pop_back();

    // Remove from the front (less efficient for vector)
    myVector.erase(myVector.begin());

    // Remove a specific element
    myVector.erase(std::remove(myVector.begin(), myVector.end(), 15), myVector.end());

    // Remove elements that satisfy a condition
    myVector.erase(std::remove_if(myVector.begin(), myVector.end(), 
                   [](int n) { return n % 2 == 0; }), myVector.end());

    // 3. Accessing elements
    if (!myVector.empty()) {
        std::cout << "First element: " << myVector.front() << std::endl;
        std::cout << "Last element: " << myVector.back() << std::endl;
    }

    // 4. Iterating through the vector
    std::cout << "Vector contents: ";
    for (const auto& elem : myVector) {
        std::cout << elem << " ";
    }
    std::cout << std::endl;

    // 5. Size operations
    std::cout << "Vector size: " << myVector.size() << std::endl;

    // 6. Clearing the vector
    myVector.clear();

    return 0;
}
```



<br/>

> When to use Vector:
>
> 1. When you need fast random access to elements.
> 2. When you primarily add or remove elements from the end.
> 3. When you want to minimize memory usage and improve cache performance.

<br/><br/>

# Comparison

### 1. Order of Elements

- Both maintains the order of elements as they are inserted.

- Both containers will iterate through elements in the same order they were inserted.

- The main difference is in how they store and access elements, not in how they maintain order.

  <br/>

### 2. Insertion and Deletion:

- List: Fast insertion and deletion anywhere in the container (O(1) time).

- Vector: Fast insertion and deletion at the end (O(1) amortized time), but slow in the middle or beginning (O(n) time).

  <br/>

### 3. Random Access:

- List: Slow random access (O(n) time).

- Vector: Fast random access (O(1) time).

  <br/>

### 4. Iterator Invalidation:

- List: Iterators remain valid after insertion or deletion.

- Vector: Iterators may be invalidated after insertion or deletion.

  <br/>

### 5. Memory Allocation:

- List: Allocates memory for each element individually.

- Vector: Allocates a contiguous block of memory.

  <br/>

### 5. Memory Overhead:

- List: Higher memory overhead due to storing pointers for each element.
- Vector: Lower memory overhead, more cache-friendly.



<br/>


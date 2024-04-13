# Programming Language Concepts
In programming, some concepts has a key role for performance, maintainability, and scalability.

# Table of Contents
1. [Mutability & Immutability In Programming Languages](#1-mutability--immutability-in-programming-languages)
   - [1.1. Mutability](#11-mutability)
   - [1.2. Immutability](#12-immutability)
   - [1.3. Examples & Use Cases](#13-examples--use-cases)
2. [Reference Type vs. Value Type](#2-reference-type-vs-value-type)
   - [2.1. Reference Types](#21-reference-types)
   - [2.2. Value Types](#22-value-types)
3. [Comparison Table](#3-comparison-table)
4. [Conclusion](#4-conclusion)


## 1. Mutability & Immutability In Programming Languages

### 1.1. Mutability
Mutable types has ability to change its state after it has been created. The state of the mutable object can be changed without creating a new instance.
Mutable objects are not inherently thread-safe. Special care (like using locks) is required when using them in a multithreaded environment. 
But mutable objects is more memory-efficient than immutable ones when value of object frequently changed. 
Also it’s more flexible than immutable objects & data types because of changing ability.

Classes, Lists, Collections, Hashsets are mutable so it's mean these collections allow adding, removing and updating.

```csharp
var list = new List<string> { "circle" };
list.Add("rectange"); 
// Now list contains "circle", "rectangle"
```

For instance, in C#, we have the mutable object StringBuilder, which is preferable when your string value changes frequently, such as with SQL Queries.
StringBuilder offers better performance due to its mutability. Unlike StringBuilder, the string data type creates a new instance with each modification after initialization.

```csharp
var builder = new StringBuilder("Hello");
builder.Append(" github!"); 
// Now builder contains "Hello github!"
// No need to create a new object
```

Classes that you define can be mutable unless you explicitly make them immutable.

```csharp
class Rectangle {
   public int Width { get; set; }
   public int Height { get; set; }
}

var rect = new Rectangle { Width = 20, Height = 15 };
rect.Width = 20; // Modifying the Width property
```

### 1.2. Immutability
Put simply, immutability in programming refers to objects whose state cannot be changed after they are created.
Immutable objects are thread safe so it can be accessed and used by multithreads concurrently. 
It’s more cache-friendly, and there is no need for synchronization in a multithreaded context. 
But immutability are not ideal for objects that can change frequently or have a large amount of data; 
so it can lead to increased use of memory due to the creation of multiple similar objects.

string, primitive data types like int, double, DateTime, etc., behave immutably.
```csharp
string greeting = "Hello";
greeting += ", World"; 
// Creates a new string, doesn't modify the original
```
Each operation on immutable types results in a new object.

```csharp
DateTime date = DateTime.Now;
date = date.AddDays(1); // Returns a new DateTime object
```

Also, there are immutable lists in some programming languages like C# :
```csharp
var immutableList = ImmutableList<int>.Empty;
immutableList = immutableList.Add(1); // Returns a new list
```

### 1.3. Examples & Use Cases

- **Use Case for ImmutableList<T> :** Consider a multi-threaded application where you need to share a list of configuration settings across different threads. 
Using ImmutableList<T> ensures that once the list is created with certain settings, it cannot be altered by any thread, 
thereby avoiding concurrency issues and ensuring consistent configuration throughout the application's lifetime. <br>

- **Use Case for List<T> :** If you have a single-threaded application or a scenario where a list is accessed and modified frequently
within the same thread (like adding items to a shopping cart in an e-commerce application), a List<T> is more appropriate.
It allows for in-place modifications without the overhead of creating a new list each time an element is added, changed, or removed.

- **Use Case for StringBuilder :** Suppose you're building a text editor or a similar application where a user's input continuously modifies a string.
Using StringBuilder allows for efficient appending, insertion, and removal of characters without the performance penalty of creating a new string with each modification.
Use Case for Immutable string : In a logging system where log messages are constructed and then never altered, using immutable strings would be more suitable.
Each log entry remains constant after creation, ensuring the integrity of the log data and simplifying debug processes.

- **Use Case for Immutable string :** In a logging system where log messages are constructed and then never altered, using immutable strings would be more suitable.
Each log entry remains constant after creation, ensuring the integrity of the log data and simplifying debug processes.

The concepts of mutable and immutable can help in making memory usage more efficient and in understanding thread-safety, concurrency, and concepts in other programming languages.

## 2. Reference Type vs. Value Type
In programming, reference and value types are two different approachs for storing and accessing data.

### 2.1. Reference Types

Reference types typically store a memory address(reference) to their data, which is actually stored in the heap.
When a reference typed variable is created, the variable stores the address of memory location that allocated on the heap. Copying a reference type means copies the address of the data, not the value itself. Therefore, multiple variables can reference the same object.
The default setting of a reference type is null, which means there is no pointed location.

```csharp
| Array: int[] |  Values: [100, 2, 3]  |
```

Memory Illustration (Heap) :
```
|  Name  |     Reference (Address)    |
|  arr1  |    Address of int[] Array  |
|  arr2  |    Address of int[] Array  |
```

### 2.2. Value Types
The copying value from a to b doesn’t affect the original value of a variable.

Integer example :
```csharp
int a = 10;
int b = a;  // Copying the value
b = 20;     // Changing b doesn't affect a
```

Memory Illustration of Variables (Stack) :
```
|  Name  |  Value  |
|   a    |   10    |
|   b    |   20    |
```

Struct Example :
```csharp
struct Point {
    public int X;
    public int Y;
}

Point p1 = new Point { X = 1, Y = 2 };
Point p2 = p1;  // Copy of p1
p2.X = 100;     // Changing p2 doesn't affect p1
```

Memory Illustration of Variables (Stack) :
```
|  Name  |  Value (X,Y) |
|   p1   |   (1, 2)     |
|   p2   |   (100, 2)   |
```

## 3. Comparison Table
| Type                                  | Type Category | Mutability  | Size (General Idea)                         |
|---------------------------------------|---------------|-------------|---------------------------------------------|
| **bool**                              | Value         | Immutable   | 1-2 bytes (depends on padding and alignment)|
| **byte**                              | Value         | Immutable   | 1 byte                                      |
| **char**                              | Value         | Immutable   | 2 bytes                                     |
| **DateTime**                          | Value         | Immutable   | ~12 bytes                                   |
| **decimal**                           | Value         | Immutable   | 16 bytes                                    |
| **double**                            | Value         | Immutable   | 8 bytes                                     |
| **float**                             | Value         | Immutable   | 4 bytes                                     |
| **Guid**                              | Value         | Immutable   | 16 bytes                                    |
| **ImmutableArray<T>**                 | Reference     | Immutable   | Depends on the type and number of elements  |
| **int**                               | Value         | Immutable   | 4 bytes                                     |
| **string**                            | Reference     | Immutable   | Depends on length of text                   |
| **Tuple<T1, T2, ...>**                | Reference     | Immutable   | Depends on the types of items stored        |
| **Uri**                               | Reference     | Immutable   | Depends on the URI length                   |
| **Array**                             | Reference     | Mutable     | Depends on the type and number of elements  |
| **ConcurrentDictionary<TKey, TValue>**| Reference     | Mutable     | Varies with elements; overhead per bucket   |
| **Dictionary<TKey, TValue>**          | Reference     | Mutable     | Varies with number of elements              |
| **HashSet<T>**                        | Reference     | Mutable     | Varies with number of elements              |
| **LinkedList<T>**                     | Reference     | Mutable     | Varies with number of elements              |
| **List<T>**                           | Reference     | Mutable     | Varies with number of elements              |
| **Queue<T>**                          | Reference     | Mutable     | Varies with number of elements              |
| **Stack<T>**                          | Reference     | Mutable     | Varies with number of elements              |
| **StringBuilder**                     | Reference     | Mutable     | Varies with size and capacity of buffer     |


## 4. Conclusion
Understanding the difference between value and reference types, especially how they are stored and managed in memory, is crucial for efficient and effective programming. 
This knowledge helps in optimizing performance, managing memory, and preventing bugs related to unintended data sharing.Also, the concepts like mutablity and immutability can help in making memory usage more efficient and thread-safe.





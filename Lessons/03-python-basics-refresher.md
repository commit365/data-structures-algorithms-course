# Lesson 3: Python Basics Refresher

## 3.1 Review of Essential Python Concepts Relevant to Data Structures

Before diving into data structures and algorithms, it's important to have a solid understanding of the fundamental concepts in Python. This section reviews essential Python features that are particularly relevant when working with data structures.

### 3.1.1 Variables and Data Types
Python supports various data types, including:
- **Integers**: Whole numbers (e.g., `5`, `-3`).
- **Floats**: Decimal numbers (e.g., `3.14`, `-0.001`).
- **Strings**: Sequences of characters (e.g., `"Hello"`, `'World'`).
- **Booleans**: Represents `True` or `False`.

### 3.1.2 Lists
Lists are one of the most commonly used data structures in Python. They are ordered, mutable collections that can hold a variety of data types.

```python
# Creating a list
my_list = [1, 2, 3, 4, 5]

# Accessing elements
print(my_list[0])  # Output: 1

# Modifying elements
my_list[1] = 10
print(my_list)  # Output: [1, 10, 3, 4, 5]
```

### 3.1.3 Tuples
Tuples are similar to lists but are immutable, meaning their elements cannot be changed after creation. They are useful for fixed collections of items.

```python
# Creating a tuple
my_tuple = (1, 2, 3)

# Accessing elements
print(my_tuple[1])  # Output: 2
```

### 3.1.4 Dictionaries
Dictionaries are key-value pairs that allow for fast data retrieval. They are unordered and mutable.

```python
# Creating a dictionary
my_dict = {'name': 'Alice', 'age': 25}

# Accessing values
print(my_dict['name'])  # Output: Alice

# Modifying values
my_dict['age'] = 26
print(my_dict)  # Output: {'name': 'Alice', 'age': 26}
```

### 3.1.5 Sets
Sets are unordered collections of unique elements. They are useful for membership testing and eliminating duplicate entries.

```python
# Creating a set
my_set = {1, 2, 3, 4, 5}

# Adding an element
my_set.add(6)
print(my_set)  # Output: {1, 2, 3, 4, 5, 6}
```

## 3.2 Introduction to Functions

Functions are reusable blocks of code that perform specific tasks. They help organize code and make it more modular.

### 3.2.1 Defining a Function
You can define a function using the `def` keyword:

```python
def greet(name):
    return f"Hello, {name}!"

# Calling a function
print(greet("Alice"))  # Output: Hello, Alice!
```

### 3.2.2 Function Parameters and Return Values
Functions can take parameters and return values. You can also provide default parameter values.

```python
def add(a, b=0):
    return a + b

print(add(5, 3))  # Output: 8
print(add(5))     # Output: 5
```

## 3.3 Modules

Modules are files containing Python code that can define functions, classes, and variables. They help organize code into manageable sections.

### 3.3.1 Importing Modules
You can import a module using the `import` statement:

```python
import math

# Using a function from the math module
print(math.sqrt(16))  # Output: 4.0
```

### 3.3.2 Creating Your Own Module
You can create your own module by saving functions in a `.py` file. For example, if you create a file named `my_module.py` with the following content:

```python
def multiply(a, b):
    return a * b
```

You can import it in another file:

```python
from my_module import multiply

print(multiply(3, 4))  # Output: 12
```

## 3.4 Error Handling

Error handling is crucial for writing robust programs. Python uses `try` and `except` blocks to handle exceptions gracefully.

### 3.4.1 Using Try and Except
You can catch exceptions and handle errors without crashing the program:

```python
try:
    result = 10 / 0
except ZeroDivisionError:
    print("You cannot divide by zero!")
```

### 3.4.2 Finally Block
You can use a `finally` block to execute code regardless of whether an exception occurred:

```python
try:
    file = open("myfile.txt", "r")
except FileNotFoundError:
    print("File not found.")
finally:
    print("Execution completed.")
```

## 3.5 Decorators

Decorators are a powerful feature in Python that allows you to modify the behavior of a function or class. They are often used for logging, access control, and caching.

### 3.5.1 Creating a Simple Decorator
Here’s how to create a simple decorator that prints a message before and after a function call:

```python
def my_decorator(func):
    def wrapper():
        print("Something is happening before the function is called.")
        func()
        print("Something is happening after the function is called.")
    return wrapper

@my_decorator
def say_hello():
    print("Hello!")

say_hello()
```

### 3.5.2 Using Decorators with Arguments
You can also create decorators that accept arguments:

```python
def repeat(num_times):
    def decorator_repeat(func):
        def wrapper(*args, **kwargs):
            for _ in range(num_times):
                func(*args, **kwargs)
        return wrapper
    return decorator_repeat

@repeat(3)
def greet(name):
    print(f"Hello, {name}!")

greet("Alice")
```

## 3.6 List Comprehensions

List comprehensions provide a concise way to create lists. They are often more readable and faster than using traditional loops.

### 3.6.1 Basic List Comprehension
Here’s an example of creating a list of squares using list comprehension:

```python
squares = [x**2 for x in range(10)]
print(squares)  # Output: [0, 1, 4, 9, 16, 25, 36, 49, 64, 81]
```

### 3.6.2 Conditional List Comprehension
You can also include conditions in list comprehensions:

```python
even_squares = [x**2 for x in range(10) if x % 2 == 0]
print(even_squares)  # Output: [0, 4, 16, 36, 64]
```

This lesson has provided a refresher on essential Python concepts relevant to data structures, including variables, data types, functions, modules, error handling, decorators, and list comprehensions. Understanding these foundational concepts will enhance your ability to work with data structures and algorithms in the upcoming lessons.

[Next: 04. Strings and String Manipulation](./04-arrays-and-lists.md)
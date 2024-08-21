# Lesson 5: Strings and String Manipulation

## 5.1 Overview of String Data Types and Their Properties

Strings are a fundamental data type in Python, representing sequences of characters. They are widely used for storing and manipulating text. Understanding string properties and operations is essential for effective programming.

### 5.1.1 Creating Strings
You can create strings in Python using single quotes, double quotes, or triple quotes for multi-line strings:

```python
# Single and double quotes
single_quote_string = 'Hello, World!'
double_quote_string = "Hello, World!"

# Triple quotes for multi-line strings
multi_line_string = """This is a 
multi-line string."""
```

### 5.1.2 Properties of Strings
- **Immutability**: Strings in Python are immutable, meaning once a string is created, it cannot be changed. Any operation that modifies a string will create a new string.

```python
original_string = "Hello"
modified_string = original_string + ", World!"  # Creates a new string
print(modified_string)  # Output: Hello, World!
```

- **Indexing**: Strings are indexed, allowing access to individual characters using their position (starting from 0).

```python
example_string = "Python"
print(example_string[0])  # Output: P
print(example_string[-1])  # Output: n (last character)
```

- **Slicing**: You can extract a substring using slicing.

```python
substring = example_string[1:4]  # Output: yth
```

### 5.1.3 Common String Methods
Python provides several built-in methods for string manipulation:

- **Length**: Get the length of a string using `len()`.

```python
length = len(example_string)  # Output: 6
```

- **Changing Case**: Convert to uppercase or lowercase.

```python
print(example_string.upper())  # Output: PYTHON
print(example_string.lower())  # Output: python
```

- **Stripping Whitespace**: Remove leading and trailing whitespace using `strip()`.

```python
whitespace_string = "   Hello, World!   "
print(whitespace_string.strip())  # Output: Hello, World!
```

- **Finding Substrings**: Check if a substring exists or find its position using `find()`.

```python
position = example_string.find("th")  # Output: 2
```

## 5.2 Common String Algorithms

### 5.2.1 Searching Strings
Searching for a substring within a string can be done using built-in methods like `find()` and `count()`.

- **Using `find()`**: Returns the index of the first occurrence of the substring or -1 if not found.

```python
text = "Hello, welcome to the world of Python."
index = text.find("welcome")  # Output: 7
```

- **Using `count()`**: Returns the number of occurrences of a substring.

```python
count = text.count("o")  # Output: 4
```

### 5.2.2 String Manipulation
Strings can be manipulated using various methods:

- **Concatenation**: Combine two strings using the `+` operator.

```python
greeting = "Hello, " + "World!"  # Output: Hello, World!
```

- **Repetition**: Repeat a string using the `*` operator.

```python
repeat_string = "Ha" * 3  # Output: HaHaHa
```

### 5.2.3 Regular Expressions
Regular expressions (regex) are powerful tools for pattern matching and string manipulation. Python provides the `re` module for working with regular expressions.

#### Example of Using Regular Expressions
```python
import re

pattern = r"\d+"  # Pattern to find one or more digits
text = "There are 123 apples and 456 oranges."

# Find all occurrences of the pattern
matches = re.findall(pattern, text)
print(matches)  # Output: ['123', '456']
```

### 5.2.4 String Matching Algorithms
String matching algorithms are used to find occurrences of a substring within a string. One popular algorithm is the **Knuth-Morris-Pratt (KMP)** algorithm, which efficiently searches for a substring in a given string.

#### Overview of the KMP Algorithm
The KMP algorithm preprocesses the pattern to create a partial match table (also known as the "prefix" table) that helps skip unnecessary comparisons during the search.

#### Basic Steps of the KMP Algorithm
1. **Preprocessing**: Create the partial match table for the pattern.
2. **Searching**: Use the table to search through the text efficiently.

#### Example Implementation of KMP Algorithm
```python
def kmp_search(text, pattern):
    # Preprocess the pattern to create the partial match table
    m = len(pattern)
    n = len(text)
    lps = [0] * m  # Longest Prefix Suffix table
    j = 0  # Index for pattern

    # Preprocessing the pattern
    for i in range(1, m):
        while j > 0 and pattern[i] != pattern[j]:
            j = lps[j - 1]
        if pattern[i] == pattern[j]:
            j += 1
            lps[i] = j
        else:
            lps[i] = 0

    # Searching the pattern in the text
    j = 0  # Index for pattern
    for i in range(n):
        while j > 0 and text[i] != pattern[j]:
            j = lps[j - 1]
        if text[i] == pattern[j]:
            j += 1
        if j == m:
            print(f"Pattern found at index {i - m + 1}")
            j = lps[j - 1]

# Example usage
text = "ababcabcabababd"
pattern = "ababd"
kmp_search(text, pattern)  # Output: Pattern found at index 10
```

This lesson provided an overview of string data types, their properties, and common string algorithms, including searching, manipulation, regular expressions, and the Knuth-Morris-Pratt string matching algorithm. Understanding these concepts is essential for effective text processing and manipulation in Python.
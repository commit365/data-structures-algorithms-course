# Lesson 7: Stacks

## 7.1 Definition and Applications of Stack Data Structures

A **stack** is a linear data structure that follows the **Last In, First Out (LIFO)** principle. This means that the last element added to the stack is the first one to be removed. Stacks are used in various applications due to their unique properties.

### 7.1.1 Characteristics of Stacks
- **Push**: The operation of adding an element to the top of the stack.
- **Pop**: The operation of removing the top element from the stack.
- **Peek (or Top)**: The operation of viewing the top element without removing it.
- **IsEmpty**: A check to determine if the stack is empty.

### 7.1.2 Applications of Stacks
Stacks have numerous practical applications, including:

- **Function Call Management**: Stacks are used to manage function calls in programming languages. Each time a function is called, its execution context is pushed onto the stack, and when the function returns, its context is popped off the stack.
- **Expression Evaluation**: Stacks are used to evaluate expressions, particularly in converting infix expressions to postfix (Reverse Polish Notation) and evaluating postfix expressions.
- **Backtracking Algorithms**: Stacks are used in algorithms that require backtracking, such as maze solving and puzzle solving.
- **Undo Mechanisms**: Many applications use stacks to implement undo functionality, where the last action can be reversed by popping the last operation from the stack.

## 7.2 Implementation of Stacks

Stacks can be implemented using various data structures, including lists and linked lists. Below, we will explore both implementations.

### 7.2.1 Stack Implementation Using Lists
Python's built-in list can be used to implement a stack easily. The `append()` method is used to push elements onto the stack, and the `pop()` method is used to remove elements.

#### Stack Class Using List
```python
class Stack:
    def __init__(self):
        self.items = []  # Initialize an empty list to store stack items

    def is_empty(self):
        return len(self.items) == 0  # Check if the stack is empty

    def push(self, item):
        self.items.append(item)  # Add an item to the top of the stack

    def pop(self):
        if self.is_empty():
            raise Exception("Stack is empty")
        return self.items.pop()  # Remove and return the top item

    def peek(self):
        if self.is_empty():
            raise Exception("Stack is empty")
        return self.items[-1]  # Return the top item without removing it

    def size(self):
        return len(self.items)  # Return the number of items in the stack
```

#### Example Usage
```python
stack = Stack()
stack.push(1)
stack.push(2)
stack.push(3)
print(stack.pop())  # Output: 3
print(stack.peek())  # Output: 2
print(stack.size())  # Output: 2
```

### 7.2.2 Stack Implementation Using Linked Lists
Stacks can also be implemented using linked lists. In this implementation, the top of the stack is represented by the head of the linked list.

#### Node Class
```python
class Node:
    def __init__(self, data):
        self.data = data  # Data part
        self.next = None  # Pointer to the next node
```

#### Stack Class Using Linked List
```python
class LinkedListStack:
    def __init__(self):
        self.head = None  # Initialize the head of the linked list

    def is_empty(self):
        return self.head is None  # Check if the stack is empty

    def push(self, item):
        new_node = Node(item)  # Create a new node
        new_node.next = self.head  # Point the new node to the current head
        self.head = new_node  # Update the head to the new node

    def pop(self):
        if self.is_empty():
            raise Exception("Stack is empty")
        popped_node = self.head  # Store the current head
        self.head = self.head.next  # Update the head to the next node
        return popped_node.data  # Return the data of the popped node

    def peek(self):
        if self.is_empty():
            raise Exception("Stack is empty")
        return self.head.data  # Return the data of the head node

    def size(self):
        count = 0
        current = self.head
        while current:
            count += 1
            current = current.next
        return count  # Return the number of items in the stack
```

#### Example Usage
```python
linked_stack = LinkedListStack()
linked_stack.push(1)
linked_stack.push(2)
linked_stack.push(3)
print(linked_stack.pop())  # Output: 3
print(linked_stack.peek())  # Output: 2
print(linked_stack.size())  # Output: 2
```

## 7.3 Practical Use Cases: Expression Evaluation

Stacks are particularly useful in evaluating expressions, especially in converting infix expressions to postfix expressions and evaluating postfix expressions.

### 7.3.1 Evaluating Postfix Expressions
A postfix expression (Reverse Polish Notation) is an expression where the operator follows all of its operands. To evaluate a postfix expression, you can use a stack as follows:

#### Algorithm for Evaluating Postfix Expressions
1. Initialize an empty stack.
2. Read the postfix expression from left to right.
3. For each token:
   - If it is a number, push it onto the stack.
   - If it is an operator, pop the top two numbers from the stack, apply the operator, and push the result back onto the stack.
4. At the end of the expression, the stack will contain one element, which is the result.

#### Example Implementation
```python
def evaluate_postfix(expression):
    stack = Stack()
    for token in expression.split():
        if token.isdigit():  # Check if the token is a number
            stack.push(int(token))
        else:  # The token is an operator
            operand2 = stack.pop()
            operand1 = stack.pop()
            if token == '+':
                result = operand1 + operand2
            elif token == '-':
                result = operand1 - operand2
            elif token == '*':
                result = operand1 * operand2
            elif token == '/':
                result = operand1 / operand2
            stack.push(result)  # Push the result back onto the stack
    return stack.pop()  # Return the final result

# Example usage
postfix_expression = "3 4 + 2 * 7 /"
result = evaluate_postfix(postfix_expression)
print(result)  # Output: 2.0
```

This lesson covered the definition and applications of stack data structures, including their implementation using lists and linked lists. Additionally, you learned about practical use cases, such as evaluating postfix expressions, demonstrating the versatility and importance of stacks in programming.

[Next: 08. Queues](./08-queues.md)
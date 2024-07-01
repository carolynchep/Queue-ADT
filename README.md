
# Queue Data Structure

Stores arbitrary elements where insertions and deletions are FIFO(First in first out)

Direct applications: waiting lines, access to a shared resource like a printer

Inderect applications : auxiliary data structure used by some algorithms and as an internal
component of other data structures

This repository contains an implementation of a generic queue data structure in Python, leveraging type hints and a custom linked list. The queue supports typical operations such as push, pop, top, and checking if the queue is empty.



## Features

- **Push**: Add an element to the end of the queue.
- **Pop**: Remove and return the front element of the queue.
- **Top**: Retrieve the front element without removing it.
- **Is Empty**: Check if the queue is empty.
- **Len**: Get the number of elements in the queue.
- **String Representation**: Get a string representation of the queue.

## Classes

### `EmptyError`

A custom exception class that extends `Exception` to handle queue-specific errors.

### `Queue`

A generic queue class that uses a linked list to manage its elements.

#### Methods

- `__init__`: Initialize an empty queue.
- `__len__`: Return the number of elements in the queue.
- `push`: Add an element to the end of the queue.
- `pop`: Remove and return the front element of the queue. Raise `EmptyError` if the queue is empty.
- `top`: Return the front element of the queue without removing it. Raise `EmptyError` if the queue is empty.
- `is_empty`: Check if the queue is empty.
- `__str__`: Return a string representation of the queue.

## Usage

### Prerequisites

Ensure you have a `LinkedList` class with the following methods:

- `add_right(item: T)`: Add an item to the right end of the list.
- `remove_left() -> T`: Remove and return the item from the left end of the list.
- `_head`: A reference to the first node in the linked list.

### Example

Here's an example of how to use the queue:

```python
from typing import Generic, TypeVar
from LinkedList import *

T = TypeVar("T")

class EmptyError(Exception):
    def __init__(self, message: str):
        self.message = message

class Queue(Generic[T]):
    __slots__ = ("_data")

    def __init__(self):
        self._data: list[T] = LinkedList()

    def __len__(self) -> int:
        return len(self._data)

    def push(self, item: T) -> None:
        self._data.add_right(item)

    def pop(self) -> T:
        if len(self._data) == 0:
            raise EmptyError('Error in Queue.pop(): queue is empty')
        return self._data.remove_left()

    def top(self) -> T:
        if len(self._data) == 0:
            raise EmptyError('Error in Queue.top(): queue is empty')
        return self._data._head.data

    def is_empty(self) -> bool:
        return len(self._data) == 0

    def __str__(self) -> str:
        string = "<- "
        a = self._data._head
        while a is not None:
            string += f"{a.data} "
            a = a.next
        string += "<-"
        return string

def main():
    MyQueue = Queue()
    MyQueue.push(11)
    MyQueue.push(33)
    MyQueue.push(40)
    print(MyQueue)
    
    print("The removed element")
    print(MyQueue.pop())
    
    print("The top element")
    print(MyQueue.top())
    
    print("The length of the queue")
    print(len(MyQueue))
    
    print("Checking if the queue is empty")
    print(MyQueue.is_empty())
    
    print("Popping all elements to empty the queue")
    MyQueue.pop()
    MyQueue.pop()
    print(MyQueue)
    
    print("Checking if the queue is empty")
    print(MyQueue.is_empty())

if __name__ == "__main__":
    main()
```
Expected Output
Running the main function should produce the following output:
```
<- 11 33 40 <-
The removed element
11
The top element
33
The length of the queue
2
Checking if the queue is empty
False
Popping all elements to empty the queue
<- <-
Checking if the queue is empty
True
```

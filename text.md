### Sort - Divide-and-Conquer

Selection Sort, Merge Sort, Count Sort, Quick Sort
Any Comparison based algorithm cannot be asymptotically faster than nlogn

Quick Sort on average is nlog\*(n), could be n^2 for worst case.
Could use random pivoits for better balanced partition.
Use 3-way partitioning for equal numbers

### Array and Lists

### Array

Definition: Contiguous arear of memory consisting of equal size elements indexed by contiguous integers.

    Constant time to add/remove at the end
    Constant-time access to any element

### Linked List

Singly-Linked List: Node contains Key, Next Pointer.
Doubly-linked List: Node contains Key, Next Pointer, Prev Pointer.

    Constant time to insert at or remove from the fromt.
    With tail and doubly-linked, conmstant time to insert at or remove from the back.
    O(n) to find arbitary element.
    List elemennts need not be contiguous.
    With doubly linked list, const time to insert between node or remove a node.

### Stacks

Occationally known as LIFO(Last In first Out) queues.
Each stack operation is O(1): Push, Pop, Top, Empty

### Queue

FIFO(First In First Out)
Abstract data type with the following operations:
Enqueue(key): adds key to teh back of collection, use List.PushBack
Key Dequeue(): removes and returns least recently-added key, use List.TopFront and List.PopFront.
Boolean Empty()
Can be implemented with eitehr a linked list (with tail pointer) or an array
Eacg queue operation is O(1).

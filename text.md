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

    Constant time to insert at or remove from the front.
    With tail and doubly-linked, conmstant time to insert at or remove from the back.
    O(n) to find arbitary element.
    List elements need not be contiguous.
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
Each queue operation is O(1).

### Trees

Trees have keys and children.
Definition: A tree is
*Empty
*a ndoe with:
*a key
*a list of child trees

Tree Walks(Tree Traversal): DFS(Pre-order, In-Order, Post-Order), and BFS.
When traversing/walking a tree, recursive algorithm is common.

Node contains:
*Key
*Children: list of children nodes
\*(optional) parent

### Binary Search Tree

Two children at each node.

\*Value of root node is GREATER than the LEFT node, and is LESS than the RIGHT node.
Leaf: Node with no children.
Interior Node: non-leaf, have children.
Level: 1+ NO. of edges bewteen root and the node.
Height: maximum depthof sub-tree node ad farthest leaf.
Forrest: Collection of trees

Binary tree node constains:
*Key
*Left
_Right
_(optional) parent

Function: Height(tree)
if (tree = nil)
return 0;
return Max(1 + Height(tree.left), 1 + + Height(tree.right))

Function: Size(tree)
if (tree = nil)
return 0;
return 1 + Size(tree.left) + Size(tree.right)

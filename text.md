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

### Tree Traversal

Visit the nodes in a particular order.
Print the nodes of the tree.

## Depth-First

Completely traverse one sub-tree before exploring a sibling sub-tree.

Implicitly uses stacks to store information about location and nodes.

Function: InOrderTraverse(tree)
if (tree = nil)
return
InOrderTraverse(tree.left)
Print(tree.key)
InOrderTraverse(tree.right)

Function: PreOrderTraverse(tree)
if (tree = nil)
return
Print(tree.key)
PreOrderTraverse(tree.left)
PreOrderTraverse(tree.right)

Function: PostOrderTraverse(tree)
if (tree = nil)
return

    PostOrderTraverse(tree.left)
    PostOrderTraverse(tree.right)
    Print(tree.key)

## Breath-First

Traverse all nodes at one level before progressing to the next.

Function: LevelTraverse(tree)
if (tree = nil), return
Queue q
q.Enqueue(tree)
while not q.Empty()
node <= q.Dequeue()
Print(node)
if (node.left != nil)
q.Enqueue(node.left)
if (node.right != nil)
q.Enqueue(node.right)

### Priority Queue

An abstract data type supporting:
Insert(p) adds a new element with priority p
ExtractMax() extracts an element with maximum proority

Unsorted Array/List
Insert() running time: O(1)
ExtractMax() running time: O(n)

Sorted Array
Insert() running time: O(n)
ExtractMax() running time: O(1)

Sorted doubly linked lists:
Insert() running time: O(n)
ExtractMax() running time: O(1)

insert is cheap since it only needs to change 4 pointers, but cannot perform binary search with lists. Therefore runnning time for insertion is O(n) for sorted list.

### Binary Heaps

Advantages:

Fast: O(log n) operations, GetMaxis O(1)

Space Efficient: Array Storage, no need to store for parent child connections

Easy to implement: few liones of code

## Binary Max Heap

Parent node >= children.
Height: Number of edges on the logest path

Operations:

GetMax: O(1), root node for the binary max heap.
Insert: O(tree hieght), attach a new node to any leaf, and then SiftUp (swap elements)
ExtractMax: O(tree height), Take out the root node and then Replace root with any leaf. SiftDown (swap with larger children until appropriate position).
ChangePriority: O(tree height), Increase/Decrease the value of the leaf, and then Sift Up/Down
Remove: O(tree heught), change the proority of the element to infinite, then extract maximum.

We want a shallow tree

## Complete Binary Tree

### JS falsy values

0;
EMpty Stirngs like "";
null;
undefined;
NaN;

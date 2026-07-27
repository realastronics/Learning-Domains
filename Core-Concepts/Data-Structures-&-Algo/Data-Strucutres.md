# Data Structures
## 0) Basic Memory Understanding

### 0.1) Stack and Heap Memory
The **stack** is a region of memory that follows **LIFO (Last In, First Out)** order, similar to a stack of books, the last one stacked on top is the first one you can pick out. In programs, the **call stack** is used to keep track of function calls.

Each function call gets its own **stack frame**, which stores: Function parameters, Local variables, & Return addresses. When a function finishes execution, its stack frame is automatically removed. Stack memory is **fast**, **limited**, and managed automatically.

The **heap** is a larger, more flexible region of memory used for data whose **lifetime cannot be determined at compile time**. Memory in the heap is **not ordered**, and objects can be accessed from anywhere in the program through references or pointers. Heap allocation is **slower** and requires explicit or automatic memory management (e.g., garbage collection).

Whether a variable is stored on the stack or heap depends on its **lifetime and usage**, not whether it is a value or reference type. If data needs to **outlive a function call**, it is typically allocated on the heap.

### 0.2) Arrays
Array is contiguous memory allocation of data, meaning information is stored next to each other in the RAM. These are the simples forms of storing data.

### 0.3) Pointers and References
Function Pointers - are regular pointers pointing to a function. A function is also just a set of instructions stored in memory.

### 0.4) Structs

Enums

### 0.5) Dynamic Memory Allocation

Unions

### 0.6) Recursion and Stack

### 0.7) Garbage Collection
Goes around head looking for things that aren’t being used anymore/occupy memory but no use and cleans them up, eg. a pointer pointing to some variable that no longer exists, the garbage collector will remove the pointer.

### 0.8) Mallocs
Malloc stands for memory allocation and is a function in C/C++ used to allocate specific amount of memory *dynamically* at runtime. It requests the memory from **heap** and returns a pointer to the first byte of the allocated space.
## 1) Time Complexity
It is the rate of which the execution time of an algorithm increases with respect to the input size (N). It is denoted by the **Big-O notation**, example:

```cpp
for ( int i = 1; i ≤ n; i ++ ) {
	cout << "Parth" ;
	}
// Every run of this code repeats the 3 steps; comparison, execution and increment. 
```

The loop runs N times, so a net of 3*N steps. **O(N)** will be the time complexity of this code block since it grows **Linearly**.

Nested loops multiply the growth:

```cpp
	for ( int i = 0; i <= N; i ++){
		for (j = 0; j <= N; j ++){
			cout << "code block";
			}
		}
// the inner loop runs N times every execution of the outer loop, which also runs N times
```

The above program has the time complexity of **$O(N^2)$.**

Always compute time complexity in terms of the worst case scenario, ignore constants and lower values. There are also theta() and omega() notations for average and the minimal complexities respectively.
## 2) Space Complexity

It is the total memory space that an algorithm takes, Auxiliary Space(memory used by the algorithm to execute) and the Input Space. Also denoted by **Big-O** notation.

## 3) Recursion

when a function calls itself until a specified condition is met. When the function goes on forever without any stop condition, it’s called infinite recursion and a stack overflow.

A base condition is put in to avoid recursion from going on forever. eg:

```cpp
#include <iostream>
using namespace std;

void printNumbers(int n) {
    // Base case
    if (n == 0) {
        return;
    }

    // Recursive call
    printNumbers(n - 1);

    // Work after recursion
    cout << n << " ";
}

int main() {
    printNumbers(5);
    return 0;
}
```

Recursion Tree
## 4) Arrays

it is a linear data structure. Continuous memory allocation. O(1) time indexing.

Continuous memory allocation, size of array = [number of those data * size of data type]. When the array

There are compile time errors which get identified before the program runs, things to the left of the = sing.
### Pattern: Running Extremes
Maintain one or more "best-so-far" values while traversing an array exactly once.
#### State
- largest
- secondLargest
#### Update Rules
1. If current element becomes the new largest:
    - old largest → second largest
    - current → largest
2. Else if current element is between largest and second largest:
    - current → second largest
#### Complexity
- Time: O(n)
- Space: O(1)
#### Problems
- Largest Element
- Second Largest
- Third Largest
### Pattern: Binary Search
Use When:
• Search space is ordered
• Looking for one answer
• Can eliminate half every step

Time:
O(log n)

Examples:
• Binary Search
• Search Insert Position
• Perfect Square
## 5) Strings

## 6) HashMaps, HashSets & Hash Arrays

### HashMap
A **HashMap** stores data as **Key → Value** pairs and provides **average O(1)** insertion, lookup, and deletion.
Unlike arrays, which use **integer indices**, a HashMap allows almost any object (Integer, String, Character, etc.) to be used as the key.

```
Key  ─────► Value

Number ───► Index
Word ─────► Frequency
StudentID ─► Name
```

Internally, a **hash function** converts a key into a bucket/index, allowing direct lookup instead of linear searching.
### Why HashMap?
Without a HashMap, searching an unsorted array requires **O(n)** time.
```text
nums = [3,2,4]
Need 2
Search → 3 → 2 ✓
```

With a HashMap:
```text
3 → 0
2 → 1
4 → 2
```

Lookup becomes approximately **O(1)**.
### Java Syntax
```java
HashMap<Integer, Integer> map = new HashMap<>();
```

Common methods:
```java
map.put(key, value);      // Insert
map.get(key);             // Retrieve value
map.containsKey(key);     // Check existence
map.remove(key);          // Remove
map.size();               // Number of entries
```
### HashSet
A **HashSet** stores **only unique values** (no key-value pairs).
```java
HashSet<Integer> set = new HashSet<>();

set.add(x);
set.contains(x);
set.remove(x);
```

Use when checking:
- Duplicate elements
- Element existence
- "Have I seen this before?"
### Hash Array (Frequency Array)
A **Hash Array** is an array used to count frequencies of **small-range integer values**.
```text
arr = [1,2,2,4,1]
freq[]

Index : 0 1 2 3 4
Value : 0 2 2 0 1
```

Meaning:
- 1 appears 2 times
- 2 appears 2 times
- 4 appears 1 time

Use only when the value range is known and small.
### HashMap vs Hash Array

| HashMap                | Hash Array                        |
| ---------------------- | --------------------------------- |
| Any key type           | Integer keys only                 |
| Dynamic size           | Fixed size                        |
| Higher memory overhead | Memory efficient for small ranges |
| O(1) average lookup    | O(1) lookup                       |
### Two Sum (Pattern)
Store:
```text
Number → Index
```

For every element:
1. Compute `need = target - current`
2. Check `map.containsKey(need)`
3. If found → return stored index and current index
4. Otherwise store `current → index`

Example:
```text
nums = [2,7,11,15]
target = 9

i=0
need=7
store 2→0

i=1
need=2
found 2→0

Answer = [0,1]
```
Time: **O(n)**  
Space: **O(n)**
### Complexity

| Structure       | Search | Insert | Delete |
| --------------- | :----: | :----: | :----: |
| Array           |  O(n)  |  O(n)  |  O(n)  |
| HashMap         | O(1)*  | O(1)*  | O(1)*  |
| HashSet         | O(1)*  | O(1)*  | O(1)*  |
| Frequency Array |  O(1)  |  O(1)  |  O(1)  |
*/*Average case.*
## 7) Linked Lists
A **Linked List** is a dynamic linear data structure consisting of **nodes**, where each node stores data and a reference to the next node. Nodes are **not stored contiguously** in memory and are accessed sequentially through references.

```
Head
 ↓
[10|•] → [20|•] → [30|null]
```
### Node
A node is the fundamental unit of a linked list.
```java
class ListNode {
    int val;
    ListNode next;
}
```
- `val` stores the data.
- `next` stores a reference to the next node.
- The final node stores `next = null`.
### Head
The **head** is a reference to the first node. Every traversal begins from the head. Losing the head reference makes the list inaccessible.
### Characteristics
- Dynamic size
- Non-contiguous memory allocation
- Sequential access only
- No direct indexing (`list[i]` is impossible)
- Extra memory required for references
### Types of Linked Lists
#### Singly Linked List
Each node points to the next node.
```
10 → 20 → 30 → null
```
#### Doubly Linked List
Each node stores references to both previous and next nodes.
```
null ← 10 ⇄ 20 ⇄ 30 → null
```
#### Circular Linked List
The last node points back to the head.
```
10 → 20 → 30
↑         ↓
└─────────┘
```
### Traversal
Traversal starts from the head and repeatedly follows the `next` reference until `null`.
```java
ListNode current = head;

while(current != null){
    current = current.next;
}
```
Traversal Complexity: **O(n)**
### Insertion
At Beginning
- `newNode.next = head`
- `head = newNode`
Time: **O(1)**

At End
- Traverse to last node.
- Update last node's `next`.
Time: **O(n)**

After Known Node
- `newNode.next = current.next`
- `current.next = newNode`
Time: **O(1)**
### Deletion
Beginning
- `head = head.next`
Time: **O(1)**

End
- Traverse to second-last node.
- Set `next = null`.
Time: **O(n)**
### Arrays vs Linked Lists

| Property                  | Array      | Linked List    |
| ------------------------- | ---------- | -------------- |
| Memory                    | Contiguous | Non-contiguous |
| Size                      | Fixed      | Dynamic        |
| Random Access             | O(1)       | O(n)           |
| Traversal                 | O(n)       | O(n)           |
| Insert/Delete (Beginning) | O(n)       | O(1)           |
| Insert/Delete (Middle)*   | O(n)       | O(1)           |
| Memory Overhead           | Low        | Higher         |

\*Assuming a reference to the insertion/deletion position is already known.
### Core Patterns
**Traversal**
- Visit every node from head to `null`.

**Reverse Linked List**
- Maintain `previous`, `current`, and `next`.
- Reverse one pointer per iteration.
- Time: **O(n)**

**Slow & Fast Pointers**
- Slow advances one node.
- Fast advances two nodes.
- Used for:
  - Middle of Linked List
  - Cycle Detection
  - Palindrome Linked List

Complexity for most operations in a Linked List is either Linear or a single operation.
### Pattern Recognition

| Requirement        | Pattern                 |
| ------------------ | ----------------------- |
| Visit every node   | Traversal               |
| Reverse links      | Previous–Current–Next   |
| Find middle        | Slow & Fast Pointers    |
| Detect cycle       | Floyd's Cycle Detection |
| Merge sorted lists | Two Pointers            |
### Common Problems
- Reverse Linked List
- Middle of Linked List
- Linked List Cycle
- Merge Two Sorted Lists
- Remove Nth Node From End
- Palindrome Linked List
## 8) Stacks

## 9) Queues

## 10) Trees
A **Tree** is a **non-linear hierarchical data structure** consisting of **nodes** connected by **edges**. A tree is an **acyclic connected graph**, i.e., there exists exactly one simple path between any two nodes.

Unlike arrays and linked lists (linear structures), trees represent **hierarchical relationships**.
### Terminology
```
        A
      /   \
     B     C
    / \
   D   E
```
- **Node** – Fundamental unit storing data.
- **Root** – Topmost node with no parent (`A`).
- **Parent** – Node with one or more children.
- **Child** – Direct descendant of a parent.
- **Sibling** – Nodes sharing the same parent (`B`, `C`).
- **Leaf (External Node)** – Node with no children (`C`, `D`, `E`).
- **Internal Node** – Node having at least one child.
- **Edge** – Connection between two nodes.
- **Subtree** – Tree rooted at any child node.
- **Ancestor** – Any node on the path from the root to a node.
- **Descendant** – Any node reachable below a node.
- **Degree of Node** – Number of children.
- **Depth** – Number of edges from the root to a node.
- **Height of Node** – Number of edges on the longest path from that node to a leaf.
- **Height of Tree** – Height of the root (longest root-to-leaf path).
### Why Trees?
Trees model naturally hierarchical data. They have various applications such as:
- File systems
- HTML/XML DOM
- Organization hierarchies
- Expression parsing
- Databases (B-Trees)
- Binary Search Trees
- Heaps
- Tries
### Binary Tree
A **Binary Tree** is a tree in which every node has **at most two children**, referred to as the **left** and **right** child.
```java
class TreeNode {
    int val;
    TreeNode left;
    TreeNode right;
}
```
A Binary Tree does **not** imply ordering.
### Binary Search Tree (BST)
A **Binary Search Tree** is a Binary Tree satisfying the ordering property:
```
Left Subtree < Root < Right Subtree
```
This property holds recursively for every subtree.

Consequences:
- Inorder traversal produces sorted order.
- Search, insertion and deletion take **O(log n)** on average.
- Worst case (skewed tree): **O(n)**.
### Types of Binary Trees
**Full Binary Tree**
- Every node has either 0 or 2 children.

**Complete Binary Tree**
- Every level is completely filled except possibly the last.
- Last level is filled from left to right.

**Perfect Binary Tree**
- Every internal node has exactly two children.
- All leaves are at the same depth.

**Balanced Binary Tree**
- Height remains approximately `O(log n)`.

**Degenerate (Skewed) Tree**
- Every node has only one child.
- Behaves like a linked list.
### Tree Traversals
Traversal is the process of visiting every node exactly once.
#### Depth First Search (DFS)
Uses recursion (implicit stack) or an explicit stack.

**Preorder**
```
Root → Left → Right
```
Applications:
- Tree copying
- Serialization
- Expression prefix notation

**Inorder**
```
Left → Root → Right
```

Applications:
- Sorted traversal of BST
- Expression trees

**Postorder**
```
Left → Right → Root
```

Applications:
- Tree deletion
- Expression evaluation
#### Breadth First Search (BFS)
Visits nodes level by level. Uses a **Queue**.

Applications:
- Level-order traversal
- Shortest path in unweighted trees
- Distance calculations
### Recursive Nature
Every subtree is itself a tree.

Most tree algorithms follow:

1. Solve left subtree.
2. Solve right subtree.
3. Combine results.

This recursive structure is fundamental to almost all tree problems.
### Complexity

| Operation | Binary Tree | BST (Average) | BST (Worst) |
| --------- | ----------- | ------------- | ----------- |
| Traversal | O(n)        | O(n)          | O(n)        |
| Search    | O(n)        | O(log n)      | O(n)        |
| Insert    | O(n)        | O(log n)      | O(n)        |
| Delete    | O(n)        | O(log n)      | O(n)        |
### Pattern Recognition

| Requirement                | Pattern   |
| -------------------------- | --------- |
| Visit every node           | DFS / BFS |
| Level-wise processing      | BFS       |
| Height / Depth             | DFS       |
| Root-to-leaf computation   | DFS       |
| Ordered search             | BST       |
| Shortest path (unweighted) | BFS       |
### Key Takeaways
- Trees are hierarchical, recursive data structures.
- Binary Trees restrict each node to at most two children.
- BSTs introduce ordering, enabling efficient search.
- DFS uses recursion/stack; BFS uses a queue.
- Most tree problems are recursive divide-and-conquer problems on subtrees.

![[tree.webp]]
## Graphs

## 5) Matrices
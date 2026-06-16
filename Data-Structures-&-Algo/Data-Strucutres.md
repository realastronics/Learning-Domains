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

## 5) Strings



## 6) HashMaps & HashSets

Hashmaps store data in key value pairs

## 7) LinkedLists

## 8) Stacks

## Qeues

## Trees

## Graphs

## 5) Matrices
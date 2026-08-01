# Algorithms

## 1) Time Complexity
It is the rate of which the execution time of an algorithm increases with respect to the input size (N). It is denoted by the **Big-O notation**, 
example:
```java
for ( int i = 1; i ≤ n; i ++ ) {
	System.out.println("Parth");
	}
// Every run of this code repeats the 3 steps; comparison, execution and increment. 
```
The loop runs N times, so a net of 3*N steps. **O(N)** will be the time complexity of this code block since it grows **Linearly**.

Nested loops multiply the growth:
```java
	for ( int i = 0; i <= N; i ++){
		for (j = 0; j <= N; j ++){
			System.out.println("code block");
			}
		}
// the inner loop runs N times every execution of the outer loop, which also runs N times
```
The above program has the time complexity of **$O(N^2)$.**

Below is the image comparing all time complexities
![[timecomplexitygraph.png]]

Always compute time complexity in terms of the worst case scenario, ignore constants and lower values since mathematically constants are insignificant relative to exponential terms. There are also theta() and omega() notations for average and the minimal complexities respectively. 
Little Omega is used for lower bound.
## 2) Space Complexity
It is the total memory space that an algorithm takes, Auxiliary Space(memory used by the algorithm to execute) and the Input Space. Also denoted by **Big-O** notation.
## 3) Recursion
When a function calls itself until a specified condition is met, it is called recursion. When the function goes on forever without any stop condition, it’s called infinite recursion and a stack overflow.

Recursion is expressed in terms of recurrences, when a function calls itself it's time complexity is described

```java
// Recursive method for the Binary Search  
class BetterBinarySearch {  
    public static int binarySearchRecursive(int[] arr, int left, int right, int target) {  
        if (left > right) {  
            return -1;  
        }  
  
        int mid = left + (right - left) / 2;  
  
        if (arr[mid] == target) {  
            return mid;  
        }  
  
        if (arr[mid] < target) {  
            return binarySearchRecursive(arr, mid + 1, right, target);  
        }  
  
        return binarySearchRecursive(arr, left, mid - 1, target);  
    }  
  
    public static void main(String[] args) {  
        int[] arr = {2, 5, 8, 12, 16, 23, 38, 56};  
        int index = binarySearchRecursive(arr, 0, arr.length - 1, 23);  
  
        if (index != -1)  
            System.out.println("Element found at index: " + index);  
        else  
            System.out.println("Element not found");  
    }  
}
```
## 4) Searching

## 5) Sorting

|Sorting|Core Idea|Time Complexity|Space|Stable?|Best Use|
|---|---|---|---|---|---|
|**Bubble Sort**|Repeatedly swap adjacent wrong elements|`O(n²)`|`O(1)`|Yes|Learning basics|
|**Selection Sort**|Find minimum and place it correctly|`O(n²)`|`O(1)`|No|Few swaps needed|
|**Insertion Sort**|Insert each element into sorted part|`O(n²)`|`O(1)`|Yes|Small/nearly sorted arrays|
|**Merge Sort**|Divide → sort → merge|`O(n log n)`|`O(n)`|Yes|Stable sorting, linked lists|
|**Quick Sort**|Pick pivot → partition → recurse|`O(n log n)` avg, `O(n²)` worst|`O(log n)`|No|Fastest in practice|
|**Heap Sort**|Use heap to repeatedly get max/min|`O(n log n)`|`O(1)`|No|Guaranteed performance|

### 1. Selection Sort - O(n^2)

1. `Read the entre array, and pick the minimum element`
2. `Swap the minimum element with the element at index [0]`
3. `Repeat using recursion with reducing array size`

```java
        int[] arr = {0, 3, 4, 2, 6, 9};
        int size = arr.length;

        // Printing the unsorted array
        System.out.print("The unsorted array is: ");
        for (int p = 0; p < size; p++){
            System.out.print(arr[p]);
        }

        // Loop to go around the entire array
        for (int i=0; i<size-1; i++) {
            int smallest = i;
            // loop for doing the comparison to find the minimum element
            for (int j= i+1; j < size - 1; j++){
                if (arr[j] < arr[smallest]){
                    smallest = j;
                }
            }

            // To swap the smallest element with the first
            int temp = arr[smallest];
            arr[smallest] = arr[i];
  0          arr[i] = temp;
62
        }
```

The primary issue is a fixed time complexity, even for an already sorted array. O(n^2) is the best, worst and the average case for this algorithm.

### 2. Bubble Sort -

The primary mechanism is swapping the adjacent elements, pushing the larger one to the right and the smaller one to the left.

```java
public class BubbleSort {
    static void bubbleSort(int[] arr) {

        int n = arr.length;
        // Outer loop for number of passes
        for (int i = 0; i < n - 1; i++) {
            boolean swapped = false;
            // Compare adjacent elements
            for (int j = 0; j < n - i - 1; j++) {
                if (arr[j] > arr[j + 1]) {
                    int temp = arr[j]; // Swap elements
                    arr[j] = arr[j + 1];
                    arr[j + 1] = temp;

                    swapped = true;
                }
            }
            // Stop early if array becomes sorted
            if (!swapped)
                break;
        }
    }

    public static void main(String[] args) {

        int[] arr = {9, 4, 7, 1, 3, 6, 2};
        System.out.println("Before Sorting:");
        for (int num : arr)
            System.out.print(num + " ");

        bubbleSort(arr);

        System.out.println("\\nAfter Sorting:");
        for (int num : arr)
            System.out.print(num + " ");
    }
```

### 3. Merge Sort: O(n log n)

- You split the array in half until you have all sorted sub-arrays (can be even down to a single element)
- Then you compare all the sub-arrays one-by-one and merge them into a single array.

Halving the array every step = log n combining each array element = n

therefore; Time Complexity = n log n

```java
void merge(int[] arr, int l, int m, int r) {
    int n1 = m - l + 1, n2 = r - m;
    int[] L = new int[n1], R = new int[n2];

    for (int i = 0; i < n1; i++) L[i] = arr[l + i];
    for (int j = 0; j < n2; j++) R[j] = arr[m + 1 + j];

    int i = 0, j = 0, k = l;
    while (i < n1 && j < n2)
        arr[k++] = (L[i] <= R[j]) ? L[i++] : R[j++];
    while (i < n1) arr[k++] = L[i++];
    while (j < n2) arr[k++] = R[j++];
}

void mergeSort(int[] arr, int l, int r) {
    if (l < r) {
        int m = (l + r) / 2;
        mergeSort(arr, l, m);
        mergeSort(arr, m + 1, r);
        merge(arr, l, m, r);
    }
}
```

### 4. Quick Sort - O(n log n)

Choose an index [i], called the **Pivot element** and sort all other elements to the left (if smaller) and right (if larger) based on the size. Repeat this as you change the pivot element to [i+1]

Comparing every element

```java
int partition(int[] arr, int low, int high) {
    int pivot = arr[high];
    int i = low - 1;
    for (int j = low; j < high; j++) {
        if (arr[j] <= pivot) {
            i++;
            int temp = arr[i]; arr[i] = arr[j]; arr[j] = temp;
        }
    }
    int temp = arr[i+1]; arr[i+1] = arr[high]; arr[high] = temp;
    return i + 1;
}

void quickSort(int[] arr, int low, int high) {
    if (low < high) {
        int pi = partition(arr, low, high);
        quickSort(arr, low, pi - 1);
        quickSort(arr, pi + 1, high);
    }
}
```

### 5. Insertion Sort - O ()

## 6) Greedy Algorithms

### 1. Fractional Knapsach O (n log n)

### 2. Huffman’s Algorithm - O (n log n)

1. Store all characters with frequencies in a min heap.
2. Repeatedly pick and merge the two minimum frequency nodes
3. Continue until only one node (Huffman Tree root) remains
4. Traverse the tree to assign binary codes (left = 0, right = 1)
5. Frequent characters get shorter codes, rare characters get longer codes

## 7) Graph Algorithms

**A tree** is just a hierarchy. One root node at the top, branches going down, leaf nodes at the bottom. Like a family tree. In Huffman, every leaf is a character.

**Prefix-free** means: no character's code is the beginning of another character's code.

### What is a Spanning Tree?

Take any connected graph, vertices connected by weighted edges. A **spanning tree** is a subgraph that:

- Connects **all** vertices
- Has **no cycles**
- Uses exactly **V-1 edges** for V vertices

There are many possible spanning trees for a graph.

A **Minimum Spanning Tree (MST)** is the one where the **total edge weight is minimum**. MST example: a telecom company laying fibre cables to connect 50 buildings — they want every building connected using **minimum total cable length. They don't care about the path between any two specific buildings, they just want the whole network connected cheaply**.

**Real world applications:**

- Laying cables/pipes to connect all buildings with minimum wire
- Designing road networks — connect all cities with minimum road length
- Network routing — minimum cost to connect all routers
- Cluster analysis in machine learning

### 1. Prim’s Algorithm - O ((v+e) log v)

Non-cyclic, **choose the next cheapest edge**, cover all vertices.

**Problem:** Connect all vertices in a weighted graph with minimum total edge cost. No cycles.

**Greedy criterion:** At each step, pick the cheapest edge that connects a visited vertex to an unvisited one.

**Why it works:** Called the Cut Property — the minimum weight edge crossing any partition of visited/unvisited vertices always belongs to some MST.

### 2. Dijkstra’s Algorithm - O ((v+e) log v)

Non-cyclic, choose the next cheapest vertex from the source considering total path, cover all vertices

**Cannot deal with negative weights** as: Once you mark a vertex as visited, you assume its distance is final. A negative edge discovered later could give a shorter path, but you've already moved on.

### 3. Kruskals’s Algorithm

**goal:** Find the MST. **Idea:** Forget starting from a vertex. Just sort ALL edges by weight and keep adding the cheapest one, as long as it doesn't create a cycle.

**Steps:**

1. Sort all edges by weight, smallest first
2. Go through edges one by one
3. If adding this edge creates a cycle → skip it
4. Otherwise → add it to MST
5. Stop when you have V-1 edges

**How do you detect a cycle?** This is where **Union-Find** comes in.

### Union-Find: the data structure Kruskal's uses

Think of it like groups. Initially every vertex is its own group.

- `find(x)` → which group does x belong to?
- `union(x, y)` → merge x's group and y's group

**Cycle detection:** If you're about to add edge (u, v) and `find(u) == find(v)` — they're already in the same group, meaning they're already connected. Adding this edge would create a cycle. Skip it.

## 8) Divide and Conquer

### Strassen's Matrix Multiplication

Normal matrix multiplication of two n×n matrices = O(n³).

Strassen's key insight: you can multiply 2×2 matrices using **7 multiplications** instead of 8, by computing clever intermediate values (p1 through p7) and combining them. This recursively gives **O(n^2.81)**.

For your exam you don't need to derive it — just know:

- Normal = O(n³)
- Strassen = O(n^2.81)
- Method = Divide and Conquer
- Why it's faster = 7 multiplications instead of 8 per recursion

## 9)Dynamic Programming (DP)

DP is used when a problem has two properties:

**1. Overlapping subproblems:** the same smaller problem gets solved multiple times if you use plain recursion.

**2. Optimal substructure:** the optimal solution to the whole problem contains optimal solutions to its subproblems.

When both are true, instead of recomputing the same subproblem repeatedly — **store the answer the first time, look it up every subsequent time.** This is called **memoization** (top-down) or building a **DP table** (bottom-up).

Greedy makes one choice and moves on. DP considers all possible choices, stores results, and picks the best.
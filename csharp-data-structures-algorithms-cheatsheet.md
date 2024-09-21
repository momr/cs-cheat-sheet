# C# Data Structures and Algorithms Cheat Sheet

## Table of Contents

- [C# Data Structures and Algorithms Cheat Sheet](#c-data-structures-and-algorithms-cheat-sheet)
  - [Table of Contents](#table-of-contents)
  - [1.0 Data Structures](#10-data-structures)
    - [1.1 Overview](#11-overview)
    - [1.2 List `List<T>`](#12-list-listt)
    - [1.3 LinkedList `LinkedList<T>`](#13-linkedlist-linkedlistt)
    - [1.4 Dictionary `Dictionary<TKey, TValue>`](#14-dictionary-dictionarytkey-tvalue)
    - [1.5 HashSet `HashSet<T>`](#15-hashset-hashsett)
    - [1.6 Stack `Stack<T>`](#16-stack-stackt)
    - [1.7 Queue `Queue<T>`](#17-queue-queuet)
    - [1.8 PriorityQueue `PriorityQueue<TElement, TPriority>`](#18-priorityqueue-priorityqueuetelement-tpriority)
  - [2.0 Trees](#20-trees)
    - [2.1 Binary Tree](#21-binary-tree)
    - [2.2 Binary Search Tree](#22-binary-search-tree)
  - [3.0 Algorithms](#30-algorithms)
    - [3.1 Binary Search](#31-binary-search)
    - [3.2 Depth-First Search (DFS)](#32-depth-first-search-dfs)
    - [3.3 Breadth-First Search (BFS)](#33-breadth-first-search-bfs)
    - [3.4 Insertion Sort](#34-insertion-sort)
    - [3.5 Quick Sort](#35-quick-sort)
    - [3.6 Merge Sort](#36-merge-sort)

## 1.0 Data Structures

### 1.1 Overview

![ComplexityChart](https://raw.githubusercontent.com/LearnSoftwareEngineering/design-patterns-in-csharp/main/assets/complexity.png "Complexity Chart")

### 1.2 List `List<T>`

**Use for**
* Dynamic array with automatic resizing
* Fast access by index
* Efficient addition/removal at the end

**Do not use for**
* Frequent insertion/deletion in the middle
* When the size is fixed and known in advance

**Time Complexity**

| Operation | Time Complexity |
| --------- | --------------- |
| Access    | O(1)            |
| Search    | O(n)            |
| Insertion | O(n)            |
| Deletion  | O(n)            |

**Example Code**
```csharp
List<int> list = new List<int>();

// Add elements
list.Add(1);
list.Add(2);
list.Add(3);

// Access by index
int element = list[1]; // Returns 2

// Insert at specific index
list.Insert(1, 4); // List is now [1, 4, 2, 3]

// Remove element
list.Remove(4); // List is now [1, 2, 3]

// Remove at index
list.RemoveAt(1); // List is now [1, 3]

// Check if element exists
bool exists = list.Contains(3); // Returns true

// Find index of element
int index = list.IndexOf(3); // Returns 1

// Iterate through list
foreach (int item in list)
{
    Console.WriteLine(item);
}

// Clear the list
list.Clear();
```

### 1.3 LinkedList `LinkedList<T>`

**Use for**
* Frequent insertion and deletion of elements
* When you need constant time insertion/deletion at both ends

**Do not use for**
* Random access to elements

**Time Complexity**

| Operation | Time Complexity |
| --------- | --------------- |
| Access    | O(n)            |
| Search    | O(n)            |
| Insertion | O(1)            |
| Deletion  | O(1)            |

**Example Code**
```csharp
LinkedList<string> linkedList = new LinkedList<string>();

// Add elements
linkedList.AddLast("Apple");
linkedList.AddLast("Banana");
linkedList.AddFirst("Cherry");

// Access first and last elements
string first = linkedList.First.Value; // Returns "Cherry"
string last = linkedList.Last.Value;   // Returns "Banana"

// Insert after a node
LinkedListNode<string> node = linkedList.Find("Apple");
linkedList.AddAfter(node, "Date");

// Remove element
linkedList.Remove("Apple");

// Check if element exists
bool exists = linkedList.Contains("Banana"); // Returns true

// Iterate through list
foreach (string fruit in linkedList)
{
    Console.WriteLine(fruit);
}

// Clear the list
linkedList.Clear();
```

### 1.4 Dictionary `Dictionary<TKey, TValue>`

**Use for**
* Key-value pairs
* Fast lookups by key
* When you need to associate data with unique keys

**Do not use for**
* Ordered data
* When you need to store duplicate keys

**Time Complexity**

| Operation | Time Complexity |
| --------- | --------------- |
| Access    | O(1) average    |
| Search    | O(1) average    |
| Insertion | O(1) average    |
| Deletion  | O(1) average    |

**Example Code**
```csharp
Dictionary<string, int> dict = new Dictionary<string, int>();

// Add key-value pairs
dict.Add("One", 1);
dict["Two"] = 2;

// Access value by key
int value = dict["One"]; // Returns 1

// Check if key exists
bool exists = dict.ContainsKey("Two"); // Returns true

// Try to get value
if (dict.TryGetValue("Three", out int result))
{
    Console.WriteLine(result);
}

// Remove key-value pair
dict.Remove("Two");

// Iterate through dictionary
foreach (KeyValuePair<string, int> kvp in dict)
{
    Console.WriteLine($"Key: {kvp.Key}, Value: {kvp.Value}");
}

// Clear the dictionary
dict.Clear();
```

### 1.5 HashSet `HashSet<T>`

**Use for**
* Storing unique elements
* Fast lookups
* When you need to check for element existence quickly

**Do not use for**
* Ordered data
* When you need to store duplicate elements

**Time Complexity**

| Operation | Time Complexity |
| --------- | --------------- |
| Access    | N/A             |
| Search    | O(1) average    |
| Insertion | O(1) average    |
| Deletion  | O(1) average    |

**Example Code**
```csharp
HashSet<int> set = new HashSet<int>();

// Add elements
set.Add(1);
set.Add(2);
set.Add(3);

// Check if element exists
bool exists = set.Contains(2); // Returns true

// Remove element
set.Remove(2);

// Iterate through set
foreach (int item in set)
{
    Console.WriteLine(item);
}

// Perform set operations
HashSet<int> otherSet = new HashSet<int> { 3, 4, 5 };
set.UnionWith(otherSet);            // Union
set.IntersectWith(otherSet);        // Intersection
set.ExceptWith(otherSet);           // Difference

// Clear the set
set.Clear();
```

### 1.6 Stack `Stack<T>`

**Use for**
* Last-In-First-Out (LIFO) operations
* Function call management
* Undo mechanisms

**Time Complexity**

| Operation | Time Complexity |
| --------- | --------------- |
| Push      | O(1)            |
| Pop       | O(1)            |
| Peek      | O(1)            |

**Example Code**
```csharp
Stack<string> stack = new Stack<string>();

// Push elements
stack.Push("First");
stack.Push("Second");
stack.Push("Third");

// Peek at the top element
string top = stack.Peek(); // Returns "Third"

// Pop element
string popped = stack.Pop(); // Returns "Third"

// Check if element exists
bool exists = stack.Contains("Second"); // Returns true

// Get number of elements
int count = stack.Count; // Returns 2

// Iterate through stack
foreach (string item in stack)
{
    Console.WriteLine(item);
}

// Clear the stack
stack.Clear();
```

### 1.7 Queue `Queue<T>`

**Use for**
* First-In-First-Out (FIFO) operations
* Breadth-First Search
* Task scheduling

**Time Complexity**

| Operation | Time Complexity |
| --------- | --------------- |
| Enqueue   | O(1)            |
| Dequeue   | O(1)            |
| Peek      | O(1)            |

**Example Code**
```csharp
Queue<int> queue = new Queue<int>();

// Enqueue elements
queue.Enqueue(1);
queue.Enqueue(2);
queue.Enqueue(3);

// Peek at the front element
int front = queue.Peek(); // Returns 1

// Dequeue element
int dequeued = queue.Dequeue(); // Returns 1

// Check if element exists
bool exists = queue.Contains(2); // Returns true

// Get number of elements
int count = queue.Count; // Returns 2

// Iterate through queue
foreach (int item in queue)
{
    Console.WriteLine(item);
}

// Clear the queue
queue.Clear();
```

### 1.8 PriorityQueue `PriorityQueue<TElement, TPriority>`

**Use for**
* Elements with associated priorities
* Task scheduling with priorities
* Dijkstra's algorithm and other graph algorithms

**Time Complexity**

| Operation | Time Complexity |
| --------- | --------------- |
| Enqueue   | O(log n)        |
| Dequeue   | O(log n)        |
| Peek      | O(1)            |

**Example Code**
```csharp
PriorityQueue<string, int> pq = new PriorityQueue<string, int>();

// Enqueue elements with priorities
pq.Enqueue("Low priority", 3);
pq.Enqueue("High priority", 1);
pq.Enqueue("Medium priority", 2);

// Peek at the highest priority element
(string element, int priority) = pq.Peek(); // Returns "High priority", 1

// Dequeue highest priority element
string dequeued = pq.Dequeue(); // Returns "High priority"

// Get number of elements
int count = pq.Count; // Returns 2

// Clear the priority queue
pq.Clear();
```

## 2.0 Trees

### 2.1 Binary Tree

A binary tree is a tree data structure in which each node has at most two children, referred to as the left child and the right child.

**Example Implementation**
```csharp
public class BinaryTreeNode<T>
{
    public T Value { get; set; }
    public BinaryTreeNode<T> Left { get; set; }
    public BinaryTreeNode<T> Right { get; set; }

    public BinaryTreeNode(T value)
    {
        Value = value;
    }
}

public class BinaryTree<T>
{
    public BinaryTreeNode<T> Root { get; set; }

    public void InOrderTraversal(Action<T> action)
    {
        InOrderTraversal(Root, action);
    }

    private void InOrderTraversal(BinaryTreeNode<T> node, Action<T> action)
    {
        if (node != null)
        {
            InOrderTraversal(node.Left, action);
            action(node.Value);
            InOrderTraversal(node.Right, action);
        }
    }
}
```

### 2.2 Binary Search Tree

A Binary Search Tree is a binary tree with the property that the value in each node is greater than or equal to any value stored in the left sub-tree, and less than or equal to any value stored in the right sub-tree.

**Example Implementation**
```csharp
public class BinarySearchTree<T> where T : IComparable<T>
{
    private BinaryTreeNode<T> root;

    public void Insert(T value)
    {
        root = InsertRec(root, value);
    }

    private BinaryTreeNode<T> InsertRec(BinaryTreeNode<T> root, T value)
    {
        if (root == null)
        {
            root = new BinaryTreeNode<T>(value);
            return root;
        }

        if (value.CompareTo(root.Value) < 0)
            root.Left = InsertRec(root.Left, value);
        else if (value.CompareTo(root.Value) > 0)
            root.Right = InsertRec(root.Right, value);

        return root;
    }

    public bool Search(T value)
    {
        return SearchRec(root, value);
    }

    private bool SearchRec(BinaryTreeNode<T> root, T value)
    {
        if (root == null || root.Value.Equals(value))
            return root != null;

        if (value.CompareTo(root.Value) < 0)
            return SearchRec(root.Left, value);

        return SearchRec(root.Right, value);
    }
}
```

## 3.0 Algorithms

### 3.1 Binary Search

**Idea:**
1. If current element, return
2. If less than current element, look left
3. If more than current element, look right
4. Repeat

**Time Complexity:** O(log n)

**Example Implementation**
```csharp
public static int BinarySearch<T>(T[] array, T value) where T : IComparable<T>
{
    int left = 0;
    int right = array.Length - 1;

    while (left <= right)
    {
        int middle = left + (right - left) / 2;
        int comparison = value.CompareTo(array[middle]);

        if (comparison == 0)
            return middle;

        if (comparison < 0)
            right = middle - 1;
        else
            left = middle + 1;
    }

    return -1; // Element not found
}
```

### 3.2 Depth-First Search (DFS)

**Idea:**
1. Start at the root (or any arbitrary node)
2. Explore as far as possible along each branch before backtracking

**Time Complexity:** O(V + E) where V is the number of vertices and E is the number of edges

**Example Implementation (for a graph)**
```csharp
public class Graph
{
    private int V; // Number of vertices
    private List<int>[] adj; // Adjacency list

    public Graph(int v)
    {
        V = v;
        adj = new List<int>[V];
        for (int i = 0; i < V; i++)
            adj[i] = new List<int>();
    }

    public void AddEdge(int v, int w)
    {
        adj[v].Add(w);
    }

    public void DFS(int v)
    {
        bool[] visited = new bool[V];
        DFSUtil(v, visited);
    }

    private void DFSUtil(int v, bool[] visited)
    {
        visited[v] = true;
        Console.Write(v + " ");

        foreach (int i in adj[v])
        {
            if (!visited[i])
                DFSUtil(i, visited);
        }
    }
}

// Usage
Graph g = new Graph(4);
g.AddEdge(0, 1);
g.AddEdge(0, 2);
g.AddEdge(1, 2);
g.AddEdge(2, 0);
g.AddEdge(2, 3);
g.AddEdge(3, 3);

Console.WriteLine("Depth First Traversal (starting from vertex 2)");
g.DFS(2);
```

### 3.3 Breadth-First Search (BFS)

**Idea:**
1. Start at the root (or any arbitrary node)
2. Explore all the neighboring nodes at the present depth before moving on to the nodes at the next depth level

**Time Complexity:** O(V + E) where V is the number of vertices and E is the number of edges

**Example Implementation (for a graph)**
```csharp
public class Graph
{
    private int V; // Number of vertices
    private List<int>[] adj; // Adjacency list

    public Graph(int v)
    {
        V = v;
        adj = new List<int>[V];
        for (int i = 0; i < V; i++)
            adj[i] = new List<int>();
    }

    public void AddEdge(int v, int w)
    {
        adj[v].Add(w);
    }

    public void BFS(int s)
    {
        bool[] visited = new bool[V];
        Queue<int> queue = new Queue<int>();

        visited[s] = true;
        queue.Enqueue(s);

        while (queue.Count != 0)
        {
            s = queue.Dequeue();
            Console.Write(s + " ");

            foreach (int i in adj[s])
            {
                if (!visited[i])
                {
                    visited[i] = true;
                    queue.Enqueue(i);
                }
            }
        }
    }
}

// Usage
Graph g = new Graph(4);
g.AddEdge(0, 1);
g.AddEdge(0, 2);
g.AddEdge(1, 2);
g.AddEdge(2, 0);
g.AddEdge(2, 3);
g.AddEdge(3, 3);

Console.WriteLine("Breadth First Traversal (starting from vertex 2)");
g.BFS(2);
```

### 3.4 Insertion Sort

**Idea:**
1. Iterate from arr[1] to arr[n] over the array
2. Compare the current element (key) to its predecessor
3. If the key element is smaller than its predecessor, compare it to the elements before. Move the greater elements one position up to make space for the swapped element.

**Time Complexity:** 
- Best Case: O(n) when the array is already sorted
- Average Case: O(n^2)
- Worst Case: O(n^2)

**Example Implementation**
```csharp
public static void InsertionSort(int[] arr)
{
    int n = arr.Length;
    for (int i = 1; i < n; ++i)
    {
        int key = arr[i];
        int j = i - 1;

        while (j >= 0 && arr[j] > key)
        {
            arr[j + 1] = arr[j];
            j = j - 1;
        }
        arr[j + 1] = key;
    }
}

// Usage
int[] arr = { 12, 11, 13, 5, 6 };
InsertionSort(arr);
Console.WriteLine("Sorted array");
foreach (int i in arr)
    Console.Write(i + " ");
```

### 3.5 Quick Sort

**Idea:**
1. Pick an element as pivot (usually the last element)
2. Partition the array around the pivot element
3. Recursively apply the above steps to the sub-arrays

**Time Complexity:**
- Best Case: O(n log n)
- Average Case: O(n log n)
- Worst Case: O(n^2) when the array is already sorted

**Example Implementation**
```csharp
public class QuickSort
{
    public static void Sort(int[] arr)
    {
        QuickSortRecursive(arr, 0, arr.Length - 1);
    }

    private static void QuickSortRecursive(int[] arr, int low, int high)
    {
        if (low < high)
        {
            int pi = Partition(arr, low, high);
            QuickSortRecursive(arr, low, pi - 1);
            QuickSortRecursive(arr, pi + 1, high);
        }
    }

    private static int Partition(int[] arr, int low, int high)
    {
        int pivot = arr[high];
        int i = (low - 1);

        for (int j = low; j < high; j++)
        {
            if (arr[j] < pivot)
            {
                i++;
                int temp = arr[i];
                arr[i] = arr[j];
                arr[j] = temp;
            }
        }

        int temp1 = arr[i + 1];
        arr[i + 1] = arr[high];
        arr[high] = temp1;

        return i + 1;
    }
}

// Usage
int[] arr = { 10, 7, 8, 9, 1, 5 };
QuickSort.Sort(arr);
Console.WriteLine("Sorted array");
foreach (int i in arr)
    Console.Write(i + " ");
```

### 3.6 Merge Sort

**Idea:**
1. Divide the unsorted list into n sublists, each containing one element (a list of one element is considered sorted)
2. Repeatedly merge sublists to produce new sorted sublists until there is only one sublist remaining

**Time Complexity:**
- Best Case: O(n log n)
- Average Case: O(n log n)
- Worst Case: O(n log n)

**Example Implementation**
```csharp
public class MergeSort
{
    public static void Sort(int[] arr)
    {
        MergeSortRecursive(arr, 0, arr.Length - 1);
    }

    private static void MergeSortRecursive(int[] arr, int left, int right)
    {
        if (left < right)
        {
            int middle = left + (right - left) / 2;
            MergeSortRecursive(arr, left, middle);
            MergeSortRecursive(arr, middle + 1, right);
            Merge(arr, left, middle, right);
        }
    }

    private static void Merge(int[] arr, int left, int middle, int right)
    {
        int n1 = middle - left + 1;
        int n2 = right - middle;

        int[] leftArray = new int[n1];
        int[] rightArray = new int[n2];

        Array.Copy(arr, left, leftArray, 0, n1);
        Array.Copy(arr, middle + 1, rightArray, 0, n2);

        int i = 0, j = 0, k = left;

        while (i < n1 && j < n2)
        {
            if (leftArray[i] <= rightArray[j])
            {
                arr[k] = leftArray[i];
                i++;
            }
            else
            {
                arr[k] = rightArray[j];
                j++;
            }
            k++;
        }

        while (i < n1)
        {
            arr[k] = leftArray[i];
            i++;
            k++;
        }

        while (j < n2)
        {
            arr[k] = rightArray[j];
            j++;
            k++;
        }
    }
}

// Usage
int[] arr = { 12, 11, 13, 5, 6, 7 };
MergeSort.Sort(arr);
Console.WriteLine("Sorted array");
foreach (int i in arr)
    Console.Write(i + " ");
```

This completes the C# Data Structures and Algorithms cheat sheet, covering essential data structures and algorithms commonly used in C# programming. The cheat sheet includes implementations, time complexities, and usage examples for each concept, providing a comprehensive reference for C# developers. 
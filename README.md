# Data Structures & Algorithms (DSA) — Interview Revision

> A structured, interview-focused revision guide for Data Structures and Algorithms.

## 📌 What is a Data Structure?

A data structure is a method of organizing and storing data so it can be accessed, modified, and processed efficiently.

### Main Categories

| Category | Organization | Examples |
|---|---|---|
| **Linear** | Elements are arranged sequentially | Array, Linked List, Stack, Queue |
| **Non-Linear** | Elements form hierarchical or interconnected relationships | Tree, Graph, Heap |

## 🎯 Why Do We Need Data Structures?

Data structures help us model complex problems, reduce unnecessary computation, manage memory efficiently, and build scalable software.

| Problem | Suitable Structure | Why |
|---|---|---|
| File-system hierarchy | Tree | Parent-child relationships |
| Social-network relationships | Graph | Many-to-many connections |
| Browser Back / Undo | Stack | Last-In-First-Out |
| Task scheduling | Queue / Priority Queue | Ordered processing |
| Fast key-value lookup | Hash Table | Average O(1) lookup |

## 🧱 Arrays

An array is a linear data structure whose elements are stored in a logically sequential arrangement. In a traditional low-level array, elements occupy contiguous memory locations.

### Memory Address Formula

If the base address is B, element size is S bytes, and the requested index is i:

Address(i) = B + (i × S)

This direct address calculation is the reason indexed access is O(1).

### Array Complexity

| Operation | Complexity | Explanation |
|---|---:|---|
| Access by index | **O(1)** | Direct address calculation |
| Update by index | **O(1)** | Direct access |
| Search by value | **O(n)** | May inspect every element |
| Insert at beginning | **O(n)** | Elements shift |
| Insert in middle | **O(n)** | Elements shift |
| Append | **O(1) amortized** | Dynamic arrays occasionally resize |
| Delete at beginning | **O(n)** | Remaining elements shift |
| Delete in middle | **O(n)** | Remaining elements shift |
| Delete at end | **O(1)** | No shifting required |

### Space Complexity

For n stored elements, the overall storage requirement is generally O(n).

## ⚠️ Traditional Static Array Limitations

1. **Fixed size** — capacity is determined when the array is created.
2. **Homogeneous type** — typed arrays normally store compatible elements of the declared type.
3. **Contiguous allocation** — a traditional array requires a suitable contiguous memory region.

## 🐍 Python Lists and Dynamic Arrays

Python list is commonly implemented as a dynamic array. It provides fast indexing, mutable length, automatic capacity management, and storage of references to Python objects.

Example:

    items = [10, 'hello', 3.14]

Python can therefore hold objects of different types in the same list because the list stores references to objects rather than requiring all objects to have the same underlying representation.

### Dynamic Resizing

When capacity is exhausted, a dynamic array allocates a larger backing area and copies/moves the existing references before continuing the operation.

An individual resize can take O(n), but repeated appends are O(1) amortized because resizing happens only occasionally.

## 🔗 Array vs Linked List

| Feature | Array / Dynamic Array | Linked List |
|---|---|---|
| Memory layout | Usually contiguous backing storage | Nodes can be non-contiguous |
| Access by index | **O(1)** | **O(n)** |
| Search by value | **O(n)** | **O(n)** |
| Insert/delete at known node | Usually **O(n)** due to shifting | **O(1)** pointer update |
| Insert/delete at beginning | **O(n)** for ordinary arrays | **O(1)** |
| Cache locality | Generally good | Generally poorer |
| Per-element overhead | Low for packed arrays | Extra node references/pointers |
| Resizing | Dynamic arrays may resize | No global resize required |

> **Interview note:** Do not say that linked lists are always faster for insertion/deletion. O(1) insertion/deletion assumes that the required node or position is already known. Finding that position can take O(n).

## 🧠 Complexity Cheat Sheet

| Complexity | Name | Typical Example |
|---|---|---|
| **O(1)** | Constant | Array index access |
| **O(log n)** | Logarithmic | Binary search |
| **O(n)** | Linear | Linear search |
| **O(n log n)** | Linearithmic | Efficient comparison sorting |
| **O(n²)** | Quadratic | Simple nested-loop comparisons |

Always evaluate both **time complexity** and **space complexity**.

## 🔍 Interview Mental Model

Use this sequence when solving a DSA problem:

**Requirements → Required operations → Data structure → Algorithm → Time complexity → Space complexity**

Ask yourself:

- Which operation happens most frequently?
- Do I need fast lookup, insertion, deletion, ordering, or traversal?
- Can I trade memory for speed?
- Is the data static or dynamic?
- What happens when n becomes very large?

## 📝 Interview Revision Checklist

- What is a data structure?
- Linear vs non-linear data structures
- Why does data structure choice affect performance?
- Why is array indexing O(1)?
- Why can array insertion/deletion be O(n)?
- What is contiguous memory?
- What is a dynamic array?
- Why is dynamic-array append O(1) amortized?
- Why can a resize operation take O(n)?
- Array vs Linked List
- Time vs space complexity
- Best structure for a given set of operations

## 🗂️ Suggested Repository Structure

    DSA-REV/
    ├── README.md
    ├── 01-Arrays/
    ├── 02-Strings/
    ├── 03-Linked-Lists/
    ├── 04-Stacks/
    ├── 05-Queues/
    ├── 06-Hashing/
    ├── 07-Recursion/
    ├── 08-Binary-Search/
    ├── 09-Sorting/
    ├── 10-Trees/
    ├── 11-Heaps/
    ├── 12-Graphs/
    ├── 13-Greedy/
    ├── 14-Backtracking/
    └── 15-Dynamic-Programming/

## 🚀 DSA Roadmap

1. Arrays
2. Strings
3. Linked Lists
4. Stacks & Queues
5. Hashing
6. Recursion
7. Binary Search
8. Sorting
9. Trees & BST
10. Heaps / Priority Queues
11. Graphs
12. Greedy Algorithms
13. Backtracking
14. Dynamic Programming

## 📚 Core Principle

> **Choose a data structure based on the operations your problem performs most often.**

The goal of DSA preparation is not to memorize isolated complexity tables. Understand **why** a data structure makes particular operations cheap or expensive, then use that understanding to design efficient solutions.

---

**Repository:** DSA-REV  •  **Focus:** Interview Revision  •  **Status:** Active Learning
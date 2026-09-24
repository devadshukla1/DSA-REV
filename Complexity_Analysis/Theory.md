# Complexity Analysis & Big O

Complexity analysis helps us understand how an algorithm behaves as the input size grows.

It is not primarily about measuring exact execution time on one machine. Instead, it describes how the amount of work and memory used by an algorithm scale with the size of the input.

---

## 1. Why Complexity Analysis Matters

Consider two ways of finding a name on a list of students.

### Method A — Check One by One

If the names are not organized, we may need to inspect each name from the beginning until the target is found.

For `N` names, the algorithm may need up to `N` checks.

This is **linear growth**: `O(N)`.

### Method B — Repeatedly Divide the Search Area

Now imagine the names are sorted alphabetically.

Instead of checking every entry, we can:

1. Look at the middle entry.
2. Decide whether the target is before or after it.
3. Discard half of the remaining entries.
4. Repeat.

Each step removes roughly half of the search space.

This gives **logarithmic growth**: `O(log N)`.

### Why This Difference Matters

For a small input, both approaches may feel equally fast. As the input becomes large, their behavior becomes very different.

| Input Size | Linear Search — O(N) | Binary Search — O(log N) |
|---:|---:|---:|
| 500 | up to 500 checks | about 9 checks |
| 5,000 | up to 5,000 checks | about 13 checks |
| 500,000 | up to 500,000 checks | about 19 checks |
| 10,000,000 | up to 10,000,000 checks | about 24 checks |

> **Key idea:** Complexity analysis is mainly about **scalability**. An algorithm that works well for 100 items may become impractical when the input reaches millions.

---

## 2. What Is Big O Notation?

**Big O notation** describes the growth of an algorithm's resource usage as the input size increases.

The expression is written as `O(f(N))`, where:

- `O` represents the order of growth.
- `N` usually represents the input size.
- `f(N)` describes how the work grows.

Big O focuses on the **growth pattern**, rather than exact machine-dependent timings.

### Example

Suppose an algorithm performs approximately `3N + 10` operations.

For large values of `N`, the constant `10` and constant multiplier `3` do not change the overall growth pattern. We therefore describe it as `O(N)`.

---

## 3. Common Time Complexity Classes

A useful progression is:

`O(1) → O(log N) → O(N) → O(N²) → O(2^N)`

### 3.1 O(1) — Constant Time

The amount of work stays approximately the same regardless of the input size.

```python
marks = [85, 90, 76, 92]

first_mark = marks[0]
```

Accessing an element by index in a Python list is typically treated as `O(1)`.

**Mental model:** one direct operation, independent of `N`.

### 3.2 O(log N) — Logarithmic Time

The algorithm repeatedly reduces the problem size, often by half.

A classic example is **binary search** on sorted data.

```python
def binary_search(names, target):
    left = 0
    right = len(names) - 1

    while left <= right:
        mid = (left + right) // 2

        if names[mid] == target:
            return mid
        elif names[mid] < target:
            left = mid + 1
        else:
            right = mid - 1

    return -1
```

At each step, about half of the remaining search space is discarded.

**Mental model:** reduce the problem instead of scanning everything.

### 3.3 O(N) — Linear Time

The amount of work grows directly with the input size.

```python
def find_name(names, target):
    for name in names:
        if name == target:
            return True

    return False
```

In the worst case, the loop examines every element.

**Mental model:** one pass through the input.

### 3.4 O(N²) — Quadratic Time

Quadratic complexity commonly appears when one loop runs inside another loop over the same input.

```python
def has_duplicate(numbers):
    n = len(numbers)

    for i in range(n):
        for j in range(n):
            if i != j and numbers[i] == numbers[j]:
                return True

    return False
```

If `N` grows, the number of comparisons can grow roughly like `N × N = N²`.

**Mental model:** compare many items against many other items.

### 3.5 O(2^N) — Exponential Time

The amount of work can approximately double whenever `N` increases by one.

Exponential growth appears in some brute-force and recursive problems, especially when each step creates multiple branches.

A common conceptual example is exploring every subset of a set, because a set of `N` elements has `2^N` possible subsets.

> Exponential algorithms can become impractical very quickly as `N` grows.

---

## 4. Time Complexity vs Space Complexity

When evaluating an algorithm, we usually care about two resources.

### Time Complexity

How the number of operations grows as the input size increases.

### Space Complexity

How much **additional memory** the algorithm needs while it runs.

These two resources can sometimes be traded against one another.

---

## 5. Space-Time Trade-Off

Consider duplicate detection.

### Approach 1 — Low Extra Space

```python
def has_duplicates_slow(numbers):
    n = len(numbers)

    for i in range(n):
        for j in range(n):
            if i != j and numbers[i] == numbers[j]:
                return True

    return False
```

Typical complexity:

- **Time:** `O(N²)`
- **Extra Space:** `O(1)`

The algorithm saves memory but performs many comparisons.

### Approach 2 — Use a Set

```python
def has_duplicates_fast(numbers):
    seen = set()

    for number in numbers:
        if number in seen:
            return True

        seen.add(number)

    return False
```

Typical average-case complexity:

- **Time:** `O(N)`
- **Extra Space:** `O(N)`

The set uses additional memory, but it provides fast average-case membership checks.

### The Main Lesson

Sometimes we can make an algorithm faster by spending more memory.

This is called a **space-time trade-off**.

> Before choosing an implementation, consider both performance requirements and available memory.

---

## 6. Best, Average, and Worst Case

The same algorithm can behave differently depending on where the target appears.

Suppose we are searching for a value in an unsorted collection of `N` items.

### Best Case

The target is found immediately.

`O(1)`

### Average Case

The target is found somewhere around the middle, depending on the input distribution.

For a simple linear scan, this is generally still described as linear growth: `O(N)`.

### Worst Case

The target is the last item, or it is not present at all.

The algorithm checks the entire collection: `O(N)`.

### Why Worst Case Is Important

Worst-case analysis tells us what resource usage can look like when the input is unfavorable.

For production systems, this matters when data size becomes large or when many requests arrive simultaneously.

---

## 7. How to Recognize Common Complexity Patterns

A useful way to estimate complexity is to look at the structure of the code.

### One Direct Operation

```python
x = arr[0]
```

→ **O(1)**

### One Loop Through N Items

```python
for x in arr:
    print(x)
```

→ **O(N)**

### Two Nested Loops Over N Items

```python
for x in arr:
    for y in arr:
        print(x, y)
```

→ **O(N²)**

### Repeatedly Halving the Search Space

```text
N → N/2 → N/4 → N/8 → ...
```

→ **O(log N)**

### Two Independent Loops

```python
for x in arr:
    ...

for y in arr:
    ...
```

This is `O(N + N)`, which simplifies to **O(N)**.

---

## 8. Practical Complexity Rules

### Ignore Constant Factors

`O(5N) → O(N)`

### Keep the Dominant Term

`O(N² + N + 10) → O(N²)`

The fastest-growing term dominates as `N` becomes large.

### Sequential Work Adds

`O(N) + O(N) = O(N)`

### Nested Work Multiplies

`O(N) × O(N) = O(N²)`

These simplifications make it easier to compare algorithms without focusing on machine-specific details.

---

## 9. Quick Complexity Reference

| Complexity | Growth Pattern | Typical Example |
|---|---|---|
| `O(1)` | Constant | Direct list/array access |
| `O(log N)` | Logarithmic | Binary search |
| `O(N)` | Linear | Single-pass search |
| `O(N log N)` | Linearithmic | Efficient comparison sorting |
| `O(N²)` | Quadratic | Nested loops |
| `O(2^N)` | Exponential | Exploring all subsets |

The table is a reference, not a rule that every algorithm must fit into exactly one category. Some algorithms have different complexities for different operations or input conditions.

---

## 10. Interview & Problem-Solving Checklist

When you finish writing a solution, ask:

1. **How many times can the main operation run?**
2. **Are there nested loops?**
3. **Am I repeatedly reducing the search space?**
4. **Am I allocating extra data structures?**
5. **What happens in the worst case?**
6. **Can I trade memory for better running time?**

A strong DSA habit is to state both:

> **Time Complexity:** `O(...)`  
> **Space Complexity:** `O(...)`

Then briefly explain **why**.

---

## 11. Core Takeaways

- Complexity analysis tells us how an algorithm scales with input size.
- Big O describes the growth pattern of resource usage.
- `O(1)` stays constant.
- `O(log N)` grows very slowly by reducing the search space.
- `O(N)` grows proportionally with the input.
- `O(N²)` often comes from nested loops.
- `O(2^N)` can become impractical very quickly.
- Time and extra space can often be traded against each other.
- Best, average, and worst cases describe different input situations.
- The goal is not to memorize labels blindly; learn to recognize the **code pattern** that produces them.

---

## Summary

The most useful question in complexity analysis is:

> **What happens to the amount of work or memory when the input becomes much larger?**

Once you can answer that question from the structure of the code, Big O becomes much easier to reason about.
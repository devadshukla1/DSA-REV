# Two-Pointer Technique

The **Two-Pointer Technique** is a common algorithmic pattern used for problems involving **searching, pair matching, array manipulation, and in-place modifications**.

Instead of using nested loops or additional data structures, the technique uses **two index variables (pointers)** to traverse a data structure according to specific rules.

Depending on the problem, Two Pointers can reduce the time complexity from **O(n²)** to **O(n)** while often using **O(1) extra space**.

---

# 1. Opposite-Direction Pattern

## Target Sum / Two-Sum

The **opposite-direction pattern** is commonly used to find two values in a **sorted array** whose sum equals a target value.

### Core Problem

Given a sorted array, find two numbers whose sum is equal to a given target.

For example:

```text
Array  = [1, 2, 3, 4, 5, 8, 11]
Target = 9
```

We need to find:

```text
1 + 8 = 9
```

---

## Brute-Force Approach

A brute-force solution checks every possible pair using nested loops.

```python
for i in range(len(arr)):
    for j in range(i + 1, len(arr)):
        if arr[i] + arr[j] == target:
            return True
```

### Complexity

```text
Time Complexity:  O(n²)
Space Complexity: O(1)
```

For `1,000` elements, this can require approximately `1,000,000` pair checks in the worst case.

---

## Two-Pointer Approach

Because the array is **sorted**, we can use two pointers.

### Pointer Placement

* **Left Pointer:** Starts at index `0`, pointing to the smallest value.
* **Right Pointer:** Starts at the last index, pointing to the largest value.

Example:

```text
Array = [1, 2, 3, 4, 5, 8, 11]

         ↑                 ↑
       Left              Right
       (1)                (11)
```

---

## Decision Logic

Calculate:

```text
sum = arr[left] + arr[right]
```

Then follow these rules:

### Case 1 — Sum Equals Target

```text
sum == target
```

The required pair has been found.

```text
1 + 8 = 9
```

---

### Case 2 — Sum Is Too Large

```text
sum > target
```

Move the **Right Pointer one position to the left**.

Why?

The right pointer currently points to a large value. Moving it left decreases the sum.

```text
right -= 1
```

---

### Case 3 — Sum Is Too Small

```text
sum < target
```

Move the **Left Pointer one position to the right**.

Why?

The left pointer currently points to a smaller value. Moving it right increases the sum.

```text
left += 1
```

---

## Step-by-Step Example

Given:

```text
Array  = [1, 2, 3, 4, 5, 8, 11]
Target = 9
```

### Initial State

```text
Left  = index 0 → 1
Right = index 6 → 11

Sum = 1 + 11
    = 12
```

Since:

```text
12 > 9
```

Move the right pointer left.

---

### Step 1

```text
Left  = index 0 → 1
Right = index 5 → 8

Sum = 1 + 8
    = 9
```

Since:

```text
9 == 9
```

The target pair is found:

```text
1 + 8 = 9
```

### Visual Representation

```text
[1, 2, 3, 4, 5, 8, 11]
 ↑              ↑
 L              R

1 + 11 = 12  → Too large
                ↓
          Move R left

[1, 2, 3, 4, 5, 8, 11]
 ↑           ↑
 L           R

1 + 8 = 9   → Target found
```

---

## Complexity Analysis

```text
Time Complexity:  O(n)
Space Complexity: O(1)
```

### Why O(n)?

Each pointer moves toward the other pointer, and neither pointer moves backward.

Therefore, the array is traversed at most linearly.

### Important Requirement

> **The opposite-direction Two-Pointer approach generally requires the array to be sorted.**

If the input is not sorted, this specific pointer movement logic does not work directly.

---

# 2. Same-Direction Pattern

## In-Place Duplicate Removal

The **same-direction pattern** is commonly used when one pointer scans the array while another pointer maintains the position where valid elements should be placed.

A classic example is:

> **Remove duplicates from a sorted array in-place.**

---

## Core Problem

Consider the following sorted array:

```text
["Aman", "Aman", "Bhavna", "Chirag", "Chirag", "Diya"]
```

The duplicate values should be removed while modifying the **original array**.

The important constraint is:

```text
Do not create another array.
```

This is called an **in-place operation**.

---

## Pointer Roles

Two pointers are used:

### Left Pointer — Slow Pointer

The `left` pointer keeps track of the position of the **last confirmed unique element**.

```text
left = 0
```

### Right Pointer — Fast Pointer

The `right` pointer scans the array from left to right.

```text
right = 1
```

---

## Initial State

```text
["Aman", "Aman", "Bhavna", "Chirag", "Chirag", "Diya"]
   ↑       ↑
 Left    Right
```

Both pointers initially help us compare the current value with the last unique value.

---

## Decision Logic

### Case 1 — Duplicate Found

If:

```python
arr[right] == arr[left]
```

The current value is a duplicate.

Therefore:

* Keep `left` where it is.
* Move `right` forward.

```python
right += 1
```

Example:

```text
["Aman", "Aman", "Bhavna", ...]
   ↑       ↑
 Left    Right

"Aman" == "Aman"
```

The second `"Aman"` is skipped.

---

### Case 2 — New Unique Value Found

If:

```python
arr[right] != arr[left]
```

A new unique value has been found.

Perform two operations:

1. Move `left` forward.
2. Copy the unique value from `right` to the new `left` position.

```python
left += 1
arr[left] = arr[right]
```

Example:

```text
["Aman", "Aman", "Bhavna", ...]
   ↑               ↑
 Left            Right

"Aman" != "Bhavna"
```

Move `left` forward:

```text
["Aman", "Aman", "Bhavna", ...]
           ↑       ↑
         Left    Right
```

Then overwrite:

```text
["Aman", "Bhavna", "Bhavna", ...]
           ↑
         Left
```

The unique values are gradually moved toward the beginning of the array.

---

## General Algorithm

For a sorted array:

```python
left = 0

for right in range(1, len(arr)):
    if arr[right] != arr[left]:
        left += 1
        arr[left] = arr[right]
```

After the loop, the unique elements occupy:

```text
index 0 → index left
```

So the number of unique elements is:

```text
left + 1
```

---

## Example

Input:

```text
["Aman", "Aman", "Bhavna", "Chirag", "Chirag", "Diya"]
```

After processing:

```text
["Aman", "Bhavna", "Chirag", "Diya", ...]
```

The meaningful portion of the array is:

```text
["Aman", "Bhavna", "Chirag", "Diya"]
```

The remaining positions are irrelevant for the standard in-place problem.

---

# Interview Significance

This pattern is closely associated with:

**LeetCode #26 — Remove Duplicates from Sorted Array**

The problem is a classic example of the **slow-and-fast pointer technique**.

It demonstrates how two pointers can modify an array **in-place without using an additional array or set**.

---

## Complexity Analysis

```text
Time Complexity:  O(n)
Space Complexity: O(1)
```

### Why O(n)?

The `right` pointer scans the array once from left to right.

Therefore, the total number of iterations is proportional to `n`.

### Why O(1) Space?

Only two pointer variables are used:

```text
left
right
```

No additional array, list, set, or other data structure is required.

---

# Two-Pointer Patterns at a Glance

| Pattern                | Pointer Movement  | Typical Use Case     | Time | Extra Space |
| ---------------------- | ----------------- | -------------------- | ---- | ----------- |
| **Opposite Direction** | Toward each other | Two-Sum / Target Sum | O(n) | O(1)        |
| **Same Direction**     | Left → Right      | Duplicate Removal    | O(n) | O(1)        |

---

# Key Takeaway

The Two-Pointer Technique is not a single algorithm. It is a **problem-solving pattern**.

The two most important patterns are:

```text
1. Opposite Direction
   ←           →
   Left       Right

2. Same Direction
   →           →
   Slow       Fast
```

### Remember

> **Opposite-direction pointers** are useful when you need to make decisions based on values at both ends of a sorted array.

> **Same-direction pointers** are useful when one pointer scans the data while another maintains the position of valid or processed elements.

The main advantage is that the technique often replaces nested loops with a **single linear scan**, reducing:

```text
O(n²) → O(n)
```

while maintaining:

```text
O(1) extra space
```

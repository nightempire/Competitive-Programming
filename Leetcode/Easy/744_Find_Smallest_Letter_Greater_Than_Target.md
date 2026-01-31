# 744. Find Smallest Letter Greater Than Target

## Platform

LeetCode

## Problem Link

[744. Find Smallest Letter Greater Than Target](https://leetcode.com/problems/find-smallest-letter-greater-than-target/)

## Problem Statement

You are given a sorted array of characters `letters` and a character `target`.

Your task is to find the **smallest character in the array that is strictly greater than `target`**.

The array is considered **circular**, meaning:

* If no character in the array is greater than `target`, return the **first character** of the array.

## Input Format

* A character array `letters` sorted in non-decreasing order
* A single character `target`

## Output Format

* Return a single character — the smallest letter strictly greater than `target`

## Constraints

* `2 ≤ letters.length ≤ 10⁴`
* `letters[i]` is a lowercase English letter
* `letters` is sorted
* `target` is a lowercase English letter

## Examples

### Example 1

Input

```
letters = ['c','f','j']
target = 'a'
```

Explanation

The smallest letter greater than `'a'` is `'c'`.

Output

```
'c'
```

---

### Example 2

Input

```
letters = ['c','f','j']
target = 'c'
```

Explanation

Letters strictly greater than `'c'` are `'f'` and `'j'`.
The smallest among them is `'f'`.

Output

```
'f'
```

---

### Example 3

Input

```
letters = ['c','f','j']
target = 'j'
```

Explanation

No letter is strictly greater than `'j'`.
Due to circular behavior, return the first letter.

Output

```
'c'
```

## Approach

**Binary Search on sorted character array**

## Intuition

Since the array is already sorted, **binary search** allows us to efficiently locate the smallest character greater than `target`.

By keeping track of a potential answer during the search, we can also handle the **wrap-around case** naturally.

## Algorithm Steps

* Initialize two pointers `low` and `high`.
* Initialize `ans` with the first character of the array.
* Perform binary search:

  * Compute `mid`.
  * If `letters[mid]` is greater than `target`:

    * Update `ans` with `letters[mid]`
    * Move search to the left half.
  * Otherwise:

    * Move search to the right half.
* Return `ans`.

## Visual Walkthrough

### Case 1

```
letters = [c, f, j]
target = c
```

Binary search:

```
mid = f → f > c → candidate
```

Final answer:

```
f
```

---

### Case 2

```
letters = [c, f, j]
target = j
```

No letter > `j`

Wrap-around:

```
return letters[0] → c
```

---

### Case 3

```
letters = [c, f, j]
target = a
```

First comparison already satisfies condition:

```
c > a
```

## Complexity Analysis

### Time Complexity

**O(log n)**

Binary search reduces the search space by half each iteration.

### Space Complexity

**O(1)**

Only constant extra variables are used.

## Solution Explanation

The solution applies binary search to efficiently find the smallest character greater than `target`.

By initializing the answer as the first element, the circular condition is handled automatically when no valid greater character is found during the search.

This makes the solution both clean and optimal.

## Full Solution

### C++ Implementation

```cpp
#include <vector>
using namespace std;

class Solution {
public:
    char nextGreatestLetter(vector<char>& letters, char target) {

        // Binary search boundaries
        int low = 0;
        int high = letters.size() - 1;

        // Default answer handles circular case
        char ans = letters[0];

        // Binary search
        while (low <= high) {

            int mid = low + (high - low) / 2;

            // If current letter is strictly greater than target
            if (letters[mid] > target) {
                ans = letters[mid];   // update answer
                high = mid - 1;       // search left half
            } else {
                low = mid + 1;        // search right half
            }
        }

        return ans;
    }
};
```

## Test Cases Analysis

| Letters | Target | Output | Reason               |
| ------- | ------ | ------ | -------------------- |
| c f j   | a      | c      | First greater letter |
| c f j   | c      | f      | Smallest greater     |
| c f j   | j      | c      | Circular wrap        |
| a b     | z      | a      | Wrap-around          |

## Edge Cases to Consider

* Target larger than all letters
* Target smaller than all letters
* Repeated characters
* Minimum array size

## Common Test Cases

* Circular wrap scenarios
* Exact character matches
* Boundary characters (`'a'`, `'z'`)

## Common Mistakes to Avoid

* Forgetting the circular condition
* Using linear search instead of binary search
* Returning `letters[low]` without bounds checking

## Interview Relevance

* Classic binary search application
* Tests understanding of circular arrays
* Frequently asked LeetCode problem

## What This Problem Teaches

* Binary search on non-numeric data
* Handling wrap-around logic cleanly
* Writing efficient search algorithms

## Key Takeaways

* Sorted data enables logarithmic solutions
* Default answers can simplify edge cases
* Binary search is versatile beyond numbers

## Problem Difficulty Analysis

This is an **Easy-to-Medium level** problem.

It combines binary search with edge-case handling, making it a common and important interview question.
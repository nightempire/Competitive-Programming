## 1855. Maximum Distance Between a Pair of Values

## Platform

LeetCode

## Problem Link

[Maximum Distance Between a Pair of Values](https://leetcode.com/problems/maximum-distance-between-a-pair-of-values/)

## Problem Statement

You are given two **non-increasing arrays** `nums1` and `nums2`.

A pair of indices `(i, j)` is considered valid if:

* `i ≤ j`
* `nums1[i] ≤ nums2[j]`

The **distance** of the pair is defined as `j - i`.

Return the **maximum distance** among all valid pairs. If no valid pair exists, return `0`.

## Input Format

* Two integer arrays `nums1` and `nums2`
* Both arrays are sorted in **non-increasing order**

## Output Format

* A single integer representing the maximum distance

## Constraints

* `1 ≤ nums1.length, nums2.length ≤ 10^5`
* `1 ≤ nums1[i], nums2[j] ≤ 10^5`
* Both arrays are sorted in **non-increasing order**

## Examples

### Example 1

Input

```
nums1 = [55,30,5,4,2]
nums2 = [100,20,10,10,5]
```

Explanation

Valid pairs include:

* `(0,0)` → 55 ≤ 100 → distance = 0
* `(2,2)` → 5 ≤ 10 → distance = 0
* `(2,4)` → 5 ≤ 5 → distance = 2

Maximum distance = **2**

Output

```
2
```

---

### Example 2

Input

```
nums1 = [2,2,2]
nums2 = [10,10,1]
```

Explanation

* `(0,1)` → 2 ≤ 10 → distance = 1
* `(1,1)` → 2 ≤ 10 → distance = 0

Maximum distance = **1**

Output

```
1
```

---

### Example 3

Input

```
nums1 = [30,29,19,5]
nums2 = [25,25,25,25,25]
```

Explanation

* `(2,4)` → 19 ≤ 25 → distance = 2
* `(3,4)` → 5 ≤ 25 → distance = 1

Maximum distance = **2**

Output

```
2
```

---

## Approach

Two Pointer Technique (Greedy Traversal on Sorted Arrays)

## Intuition

Since both arrays are sorted in **non-increasing order**, we can efficiently traverse them using two pointers:

* If a pair is valid, try to expand the distance by moving `j` forward.
* If invalid, move `i` forward to find a smaller value in `nums1`.

This avoids brute-force `O(n^2)` comparisons.

## Algorithm Steps

* Initialize two pointers `i = 0`, `j = 0`

* Initialize `maxi = 0`

* While both pointers are within bounds:

  * If `nums1[i] ≤ nums2[j]`:

    * Update `maxi = max(maxi, j - i)`
    * Move `j++` to increase distance
  * Else:

    * Move `i++` to reduce `nums1[i]`
    * Ensure `j ≥ i` (adjust `j = i` if needed)

* Return `maxi`

## Visual Walkthrough

### Case 1

```
nums1 = [55,30,5]
nums2 = [100,20,10]
```

```
i=0, j=0 → 55 ≤ 100 → valid → distance = 0
i=0, j=1 → 55 ≤ 20 → invalid → move i
i=1, j=1 → 30 ≤ 20 → invalid → move i
i=2, j=2 → 5 ≤ 10 → valid → distance = 0
```

---

### Case 2

```
nums1 = [5,4]
nums2 = [10,9,8]
```

```
i=0, j=0 → valid → dist=0
i=0, j=1 → valid → dist=1
i=0, j=2 → valid → dist=2 (max)
```

---

### Case 3

```
nums1 = [10,9]
nums2 = [5,4]
```

```
All invalid → result = 0
```

## Complexity Analysis

### Time Complexity

**O(n + m)**

Each pointer (`i`, `j`) moves at most once through its respective array.
No nested iteration occurs.

### Space Complexity

**O(1)**

Only constant extra variables are used.

## Solution Explanation

The solution efficiently leverages the sorted nature of the arrays. By maintaining two pointers, it avoids redundant comparisons and ensures that every valid pair is considered exactly once. The adjustment `if (i > j) j = i` guarantees correctness of index constraints.

## Full Solution

### C++ Implementation

```cpp
#include <iostream>
#include <vector>
using namespace std;

class Solution {
public:
    int maxDistance(vector<int>& nums1, vector<int>& nums2) {

        // Pointer for nums1
        int i = 0;

        // Pointer for nums2
        int j = 0;

        // Sizes of arrays
        int n = nums1.size();
        int m = nums2.size();

        // Variable to store maximum distance
        int maxi = 0;

        // Traverse both arrays
        while (i < n && j < m) {

            // If valid condition is satisfied
            if (nums1[i] <= nums2[j]) {

                // Update maximum distance
                maxi = max(maxi, j - i);

                // Move j forward to increase distance
                j++;
            }
            else {

                // Move i forward to reduce nums1[i]
                i++;

                // Ensure j is always >= i
                // (because j must not be less than i)
                if (i > j)
                    j = i;
            }
        }

        // Return the result
        return maxi;
    }
};
```

## Test Cases Analysis

| nums1        | nums2            | Valid Pair Example | Output |
| ------------ | ---------------- | ------------------ | ------ |
| [55,30,5]    | [100,20,10]      | (2,2)              | 0      |
| [2,2,2]      | [10,10,1]        | (0,1)              | 1      |
| [30,29,19,5] | [25,25,25,25,25] | (2,4)              | 2      |
| [10,9]       | [5,4]            | None               | 0      |

## Edge Cases to Consider

* No valid pair exists
* Arrays of size 1
* All elements equal
* Large inputs (performance check)

## Common Test Cases

* Strictly decreasing arrays
* Fully valid arrays (all pairs valid)
* Completely invalid arrays
* Mixed valid and invalid conditions

## Common Mistakes to Avoid

* Forgetting the constraint `i ≤ j`
* Not adjusting `j` when `i` increases
* Using brute-force leading to TLE

## Interview Relevance

* Classic **two-pointer optimization problem**
* Tests understanding of sorted array properties
* Evaluates greedy reasoning

## What This Problem Teaches

* Efficient traversal using two pointers
* Leveraging sorted data for optimization
* Avoiding unnecessary comparisons

## Key Takeaways

* Two-pointer technique can reduce complexity drastically
* Always exploit input constraints (sorted arrays)
* Maintain invariants like `i ≤ j`

## Problem Difficulty Analysis

This is a **Medium-level** problem.

While the logic is not complex, identifying the correct two-pointer strategy and handling pointer adjustments correctly requires solid problem-solving skills.
# 3719. Longest Balanced Subarray I

## Platform

LeetCode

## Problem Link

[3719. Longest Balanced Subarray I](https://leetcode.com/problems/longest-balanced-subarray-i/)

## Problem Statement

You are given an integer array `nums`.

A subarray is called **balanced** if the **number of distinct odd elements** in the subarray is equal to the **number of distinct even elements** in the subarray.

Your task is to return the **maximum length** of a balanced subarray.

If no balanced subarray exists, return `0`.

## Input Format

* A single integer array `nums`

## Output Format

* Return an integer representing the length of the longest balanced subarray

## Constraints

* `1 ≤ nums.length ≤ 100`
* `1 ≤ nums[i] ≤ 10^9`

## Examples

### Example 1

Input

```
[1, 2, 3, 4]
```

Explanation

Consider all subarrays:

* `[1, 2]`

  * Odd distinct = `{1}` → 1
  * Even distinct = `{2}` → 1 → balanced (length 2)
* `[1, 2, 3, 4]`

  * Odd distinct = `{1, 3}` → 2
  * Even distinct = `{2, 4}` → 2 → balanced (length 4)

Output

```
4
```

---

### Example 2

Input

```
[2, 4, 6]
```

Explanation

All elements are even:

* Odd distinct count = 0
* Even distinct count > 0

No balanced subarray exists.

Output

```
0
```

---

### Example 3

Input

```
[1, 1, 2, 2]
```

Explanation

Subarray `[1, 1, 2, 2]`:

* Odd distinct = `{1}` → 1
* Even distinct = `{2}` → 1

Balanced with length 4.

Output

```
4
```

## Approach

**Brute Force Subarray Enumeration with Distinct Tracking**

## Intuition

The balance condition depends on:

* The **count of distinct odd numbers**
* The **count of distinct even numbers**

Since distinctness matters, we must explicitly track elements inside each subarray.

The idea:

* Fix a starting index
* Extend the subarray one element at a time
* Maintain two sets:

  * One for odd numbers
  * One for even numbers
* At each step, check if their sizes are equal

## Algorithm Steps

* Initialize `mx = 0`
* For every starting index `i`:

  * Create empty sets `odd` and `even`
  * For every ending index `j ≥ i`:

    * If `nums[j]` is odd, insert into `odd`
    * Else, insert into `even`
    * If `odd.size() == even.size()`:

      * Update `mx` with `j - i + 1`
* Return `mx`

## Visual Walkthrough

### Case 1: `[1, 2, 3]`

```
Start i = 0
Subarray [1] → odd=1, even=0 → not balanced
Subarray [1,2] → odd=1, even=1 → balanced (len=2)
Subarray [1,2,3] → odd=2, even=1 → not balanced
```

---

### Case 2: `[2, 3]`

```
Subarray [2] → odd=0, even=1 → not balanced
Subarray [2,3] → odd=1, even=1 → balanced (len=2)
```

---

### Case 3: `[1, 1, 2]`

```
Subarray [1,1,2]
odd={1} → 1
even={2} → 1
Balanced
```

## Complexity Analysis

### Time Complexity

**O(n²)**

All subarrays are examined, and each insertion into a set is amortized constant time.

### Space Complexity

**O(n)**

Sets may store up to `n` distinct elements in the worst case.

## Solution Explanation

The solution explicitly checks every possible subarray.

For each subarray:

* Two sets are maintained to ensure **distinct counting**
* The balance condition is verified at every extension

Although brute force, this approach is sufficient due to small input constraints and directly follows the problem definition.

## Full Solution

### C++ Implementation

```cpp
class Solution {
public:
    int longestBalanced(vector<int>& nums) {

        // Variable to store maximum balanced subarray length
        int mx = 0;

        // Fix the starting index
        for (int i = 0; i < nums.size(); i++) {

            // Sets to track distinct odd and even elements
            unordered_set<int> odd, even;

            // Extend subarray to the right
            for (int j = i; j < nums.size(); j++) {

                // Insert element into appropriate set
                if (nums[j] & 1)
                    odd.insert(nums[j]);
                else
                    even.insert(nums[j]);

                // Check balanced condition
                if (odd.size() == even.size()) {
                    mx = max(mx, j - i + 1);
                }
            }
        }

        return mx;
    }
};
```

## Test Cases Analysis

| Input Array | Balanced Subarray | Output |
| ----------- | ----------------- | ------ |
| `[1,2,3,4]` | Entire array      | 4      |
| `[2,4,6]`   | None              | 0      |
| `[1,1,2,2]` | Entire array      | 4      |
| `[1,3,5,2]` | `[3,5,2]`         | 3      |

## Edge Cases to Consider

* Array with only odd elements
* Array with only even elements
* Repeated values
* Single-element array

## Common Test Cases

* Alternating odd and even values
* Arrays with duplicates
* Small-sized arrays

## Common Mistakes to Avoid

* Counting total odd/even instead of **distinct**
* Forgetting to reset sets for each starting index
* Using frequency instead of uniqueness

## Interview Relevance

* Tests understanding of subarrays
* Evaluates handling of distinct elements
* Reinforces brute-force feasibility analysis

## What This Problem Teaches

* Importance of understanding problem constraints
* Distinction between frequency and uniqueness
* Trade-offs between brute force and optimization

## Key Takeaways

* Distinct counts require set-based tracking
* Brute force is acceptable under tight constraints
* Clear interpretation of “balanced” is critical

## Problem Difficulty Analysis

This is an **Easy-to-Medium level** problem.

The logic is straightforward, but careful handling of distinct elements and nested loops is required to avoid incorrect assumptions.
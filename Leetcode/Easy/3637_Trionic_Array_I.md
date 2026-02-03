# Trionic Array I

## Platform

LeetCode

## Problem Link

[3637. Trionic Array I](https://leetcode.com/problems/trionic-array-i/)

## Problem Statement

You are given an integer array `nums`.

An array is called **trionic** if it can be divided into **three consecutive non-empty segments** such that:

* The **first segment is strictly increasing**
* The **second segment is strictly decreasing**
* The **third segment is strictly increasing**

Additionally:

* No two adjacent elements in the array are equal
* The transitions between segments must occur at valid positions

Your task is to determine whether the given array `nums` is a **trionic array**.

Return `true` if it is trionic, otherwise return `false`.

## Input Format

* A single integer array `nums`

## Output Format

* Return a boolean value:

  * `true` if `nums` is a trionic array
  * `false` otherwise

## Constraints

* `3 ≤ nums.length ≤ 10^5`
* `-10^9 ≤ nums[i] ≤ 10^9`

## Examples

### Example 1

Input

```
nums = [1, 3, 5, 4, 2, 6, 8]
```

Explanation

* First segment (increasing): `1 → 3 → 5`
* Second segment (decreasing): `5 → 4 → 2`
* Third segment (increasing): `2 → 6 → 8`

All conditions are satisfied.

Output

```
true
```

### Example 2

Input

```
nums = [1, 2, 3, 4]
```

Explanation

* The array is only increasing
* Missing a decreasing segment

Output

```
false
```

### Example 3

Input

```
nums = [1, 3, 3, 2, 4]
```

Explanation

* Adjacent equal elements (`3 == 3`) are not allowed

Output

```
false
```

## Approach

**Single-pass segmented monotonic scan**

## Intuition

A trionic array must follow a **strict pattern**:

```
Increasing → Decreasing → Increasing
```

The idea is to:

* Detect the first position where increasing breaks (start of decreasing)
* Detect the first position where decreasing breaks (start of final increasing)
* Validate strict monotonicity in all three segments
* Ensure each segment is non-empty and properly ordered

Any violation immediately invalidates the array.

## Algorithm Steps

* Traverse the array to find the first index `p` where the sequence stops increasing
* Validate that the first segment is non-empty
* From `p`, find the first index `q` where the sequence stops decreasing
* Validate that the second segment is non-empty
* From `q`, ensure the remaining elements are strictly increasing
* At any point, if adjacent elements are equal, return `false`
* If all checks pass, return `true`

## Visual Walkthrough

### Test Case 1

```
[1, 4, 7, 5, 3, 6, 9]
```

Segments:

```
Increasing : 1 → 4 → 7
Decreasing : 7 → 5 → 3
Increasing : 3 → 6 → 9
```

Result:

```
true
```

---

### Test Case 2

```
[5, 4, 3, 2, 1]
```

Observation:

```
Missing first increasing segment
```

Result:

```
false
```

---

### Test Case 3

```
[1, 2, 3, 2, 2, 4]
```

Observation:

```
Adjacent equal values detected (2 == 2)
```

Result:

```
false
```

## Complexity Analysis

### Time Complexity

**O(n)**

* The array is traversed at most once
* Each element is checked a constant number of times

### Space Complexity

**O(1)**

* Only a few integer variables are used
* No extra memory proportional to input size is required

## Solution Explanation

The solution identifies two critical turning points:

* `p`: transition from increasing to decreasing
* `q`: transition from decreasing to increasing

By enforcing strict comparisons (`<` and `>`) and rejecting equality early, the algorithm ensures all three segments satisfy the trionic definition.
Each segment’s validity is checked sequentially, making the solution both efficient and easy to reason about.

## Full Solution

### C++ Implementation

```cpp
class Solution {
public:
    bool isTrionic(vector<int>& nums) {

        int n = nums.size();

        // p marks the end of the first increasing segment
        // q marks the end of the decreasing segment
        int p = -1, q = -1;

        // Step 1: Find where increasing breaks
        for (int i = 0; i < n - 1; i++) {

            // Equal adjacent elements are not allowed
            if (nums[i] == nums[i + 1]) return false;

            // First drop indicates transition to decreasing
            if (nums[i] > nums[i + 1]) {
                p = i;
                break;
            }
        }

        // First segment must be non-empty
        if (p == -1 || p == 0) return false;

        // Step 2: Find where decreasing breaks
        for (int i = p + 1; i < n - 1; i++) {

            // Equal adjacent elements are not allowed
            if (nums[i] == nums[i + 1]) return false;

            // Rise indicates transition to final increasing
            if (nums[i] < nums[i + 1]) {
                q = i;
                break;
            }
        }

        // Second segment must be non-empty
        if (q == -1 || q == n - 1) return false;

        // Step 3: Ensure final segment is strictly increasing
        for (int i = q + 1; i < n - 1; i++) {

            if (nums[i] >= nums[i + 1]) {
                return false;
            }
        }

        return true;
    }
};
```

## Test Cases Analysis

| Test Case | Input Array     | Expected Output |
| --------- | --------------- | --------------- |
| 1         | [1,3,5,4,2,6,8] | true            |
| 2         | [1,2,3,4]       | false           |
| 3         | [5,4,3,2,1]     | false           |
| 4         | [1,2,3,2,2,4]   | false           |
| 5         | [1,4,7,6,3,5]   | true            |

## Edge Cases to Consider

* All elements strictly increasing
* All elements strictly decreasing
* Adjacent equal elements anywhere
* Very small arrays near minimum size

## Common Test Cases

* Proper three-segment monotonic arrays
* Arrays missing one of the required segments
* Arrays with plateaus (equal adjacent values)

## Common Mistakes to Avoid

* Allowing equality in comparisons
* Not ensuring segments are non-empty
* Incorrectly detecting transition points

## Interview Relevance

* Tests array traversal and pattern recognition
* Evaluates careful boundary handling
* Common variation of monotonic sequence problems

## What This Problem Teaches

* How to detect structured patterns in arrays
* Importance of strict inequalities
* Clean segmentation logic in linear time

## Key Takeaways

* Early validation simplifies logic
* Segment boundaries are critical
* Linear scans are often sufficient for pattern problems

## Problem Difficulty Analysis

This is a **Medium-level** problem.
While the logic is linear, careful handling of transitions and edge cases is required to avoid subtle bugs.
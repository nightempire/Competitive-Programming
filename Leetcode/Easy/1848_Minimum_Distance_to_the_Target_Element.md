## Platform

LeetCode

## Problem Link

[1848. Minimum Distance to the Target Element](https://leetcode.com/problems/minimum-distance-to-the-target-element)

---

## Problem Statement

You are given:

* An integer array `nums`
* An integer `target`
* An integer `start`

Your task is to find the **minimum distance** between index `start` and any index `i` such that:

```text
nums[i] == target
```

Distance is defined as:

```text
|i - start|
```

Return the minimum such distance.

---

## Input Format

* Integer array `nums`
* Integer `target`
* Integer `start`

---

## Output Format

* Return an integer — minimum distance

---

## Constraints

* `1 ≤ nums.length ≤ 1000`
* `1 ≤ nums[i] ≤ 10^4`
* `0 ≤ start < nums.length`
* `target` exists in `nums`

---

## Examples

### Example 1

Input

```id="u2k9mz"
nums = [1,2,3,4,5]
target = 5
start = 3
```

Explanation

* Index of target = 4
* Distance = |4 - 3| = 1

Output

```id="p7x4qc"
1
```

---

### Example 2

Input

```id="k3n8vd"
nums = [1]
target = 1
start = 0
```

Explanation

* Already at target

Output

```id="z5m2rt"
0
```

---

### Example 3

Input

```id="v6q1xp"
nums = [1,1,1,1,1,1]
target = 1
start = 2
```

Explanation

* Target exists at start

Output

```id="t8k4zs"
0
```

---

## Approach

Bidirectional search from starting index

---

## Intuition

Instead of scanning the entire array, we expand outward from `start`:

* Check left and right simultaneously
* As soon as we find `target`, we return distance

This guarantees:

* First occurrence found → minimum distance

---

## Algorithm Steps

* If `nums[start] == target`:

  * Return `0`
* Initialize:

  * `left = start - 1`
  * `right = start + 1`
* While either pointer is valid:

  * If `left` is valid and `nums[left] == target`:

    * Return `start - left`
  * If `right` is valid and `nums[right] == target`:

    * Return `right - start`
  * Move:

    * `left--`
    * `right++`

---

## Visual Walkthrough

### Case 1

```id="g7m3pz"
nums = [1,2,3,4,5]
start = 3

Check:
left → index 2 → 3
right → index 4 → 5 → match

Distance = 1
```

---

### Case 2

```id="r4k8xt"
nums = [1]
start = 0

Already target → distance = 0
```

---

### Case 3

```id="m9p2vz"
nums = [1,1,1,1]
start = 2

Immediate match → distance = 0
```

---

## Complexity Analysis

### Time Complexity

O(n)

* Worst case scans entire array

---

### Space Complexity

O(1)

* No extra memory used

---

## Solution Explanation

The solution uses a **two-pointer expansion strategy**:

* Start from `start`
* Expand outward
* Check both sides at each step

This ensures:

* The first match found is the closest one

---

## Full Solution

### C++ Implementation

```cpp id="q6k3mz"
#include <vector>
using namespace std;

class Solution {
public:
    int getMinDistance(vector<int>& nums, int target, int start) {

        // If starting index already has target
        if(nums[start] == target) return 0;

        int n = nums.size();

        // Initialize pointers
        int left = start - 1;
        int right = start + 1;

        // Expand outward
        while(left >= 0 || right < n) {

            // Check left side
            if(left >= 0 && nums[left] == target) {
                return start - left;
            }

            // Check right side
            if(right < n && nums[right] == target) {
                return right - start;
            }

            // Move pointers
            if(left >= 0) left--;
            if(right < n) right++;
        }

        // Should not reach here (target guaranteed)
        return -1;
    }
};
```

---

## Test Cases Analysis

| nums        | target | start | Result |
| ----------- | ------ | ----- | ------ |
| [1,2,3,4,5] | 5      | 3     | 1      |
| [1]         | 1      | 0     | 0      |
| [1,1,1,1]   | 1      | 2     | 0      |
| [2,3,4,2,5] | 2      | 2     | 1      |

---

## Edge Cases to Consider

* Target at start index
* Target appears multiple times
* Target only on one side
* Small array size

---

## Common Test Cases

* Single element array
* Multiple occurrences of target
* Target far from start

---

## Common Mistakes to Avoid

* Scanning entire array unnecessarily
* Not checking start index first
* Incorrect boundary handling

---

## Interview Relevance

* Two-pointer techniques
* Optimal search strategies
* Problem simplification

---

## What This Problem Teaches

* Expanding search technique
* Efficient nearest-element finding
* Avoiding brute-force scans

---

## Key Takeaways

* Start from closest point (start index)
* Expand outward for minimum distance
* Two-pointer approach is optimal

---

## Problem Difficulty Analysis

This is an **Easy-level** problem.

It focuses on:

* Array traversal
* Two-pointer logic
* Efficient searching
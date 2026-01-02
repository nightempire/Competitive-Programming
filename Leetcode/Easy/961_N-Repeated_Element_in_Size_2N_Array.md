# 961. N-Repeated Element in Size 2N Array

## Platform

LeetCode

## Problem Link

[961. N-Repeated Element in Size 2N Array](https://leetcode.com/problems/n-repeated-element-in-size-2n-array/)

## Problem Statement

You are given an integer array `nums` of length `2N`.

Exactly **one element is repeated `N` times**, while all other elements appear exactly once.

Your task is to **identify and return the element that is repeated `N` times**.

## Input Format

* A vector of integers `nums`
* Length of `nums` is `2N`

## Output Format

* Return the integer that appears `N` times

## Constraints

* `2 ≤ nums.length ≤ 10^4`
* `nums.length` is even
* Exactly one element appears `N` times
* Other elements appear once

## Examples

### Example 1

Input

```
[1,2,3,3]
```

Explanation
`3` appears twice (`N = 2`).

Output

```
3
```

### Example 2

Input

```
[2,1,2,5,3,2]
```

Explanation
`2` appears three times (`N = 3`).

Output

```
2
```

### Example 3

Input

```
[5,1,5,2,5,3,5,4]
```

Explanation
`5` appears four times.

Output

```
5
```

## Approach

**Approach 1: Hash Set Detection**
**Approach 2: Adjacent Comparison Observation**

## Intuition

Because one element appears `N` times in an array of size `2N`, repetitions must occur **very frequently**.

* Using a set allows immediate detection of duplicates.
* Observing array structure reveals that the repeated element must appear close to itself (within distance ≤ 2).

Both insights lead to efficient solutions.

## Algorithm Steps

### Approach 1

* Create an empty hash set
* Traverse the array
* Try inserting each element into the set
* If insertion fails, that element is the repeated one
* Return immediately

### Approach 2

* Traverse the array starting from index `2`
* Check if the current element matches either of the two previous elements
* If matched, return it
* If no match found in loop, return the last element

## Visual Walkthrough

Input:

```
[2,1,2,5,3,2]
```

Approach 1:

```
Insert 2 → ok
Insert 1 → ok
Insert 2 → already exists → answer
```

Approach 2:

```
Index 2: nums[0] == nums[2] → 2 == 2 → answer
```

Another case:

```
[5,1,5,2,5,3,5,4]
```

Repeated element appears every few positions → guaranteed early detection.

## Complexity Analysis

### Approach 1

Time Complexity
O(n)
Each insertion and lookup in a hash set is O(1) on average.

Space Complexity
O(n)
Extra space used for the hash set.

### Approach 2

Time Complexity
O(n)
Single pass through the array.

Space Complexity
O(1)
No extra data structures used.

## Solution Explanation

### Approach 1 Explanation

The hash set ensures uniqueness.
The moment an insertion fails, the repeated element is identified.
This approach is simple and intuitive.

### Approach 2 Explanation

Due to the constraint that one number appears `N` times, it is mathematically guaranteed that the repeated number will appear adjacent to itself or with at most one element in between.
Checking only the previous two elements is sufficient to detect it.

This approach is optimal in both time and space.

## Full Solution

### Approach 1: Using Hash Set

```cpp
class Solution {
public:
    int repeatedNTimes(vector<int>& nums) {

        // Hash set to track seen elements
        unordered_set<int> s;

        // Traverse the array
        for (int num : nums) {

            // Try inserting the number into the set
            // insert() returns a pair; second = false if already exists
            if (!s.insert(num).second) {
                return num;  // Found the repeated element
            }
        }

        // This line should never be reached due to problem guarantees
        return -1;
    }
};
```

### Approach 2: Constant Space Observation

```cpp
class Solution {
public:
    int repeatedNTimes(vector<int>& nums) {

        // Start checking from index 2
        for (int i = 2; i < nums.size(); i++) {

            // If the current element matches either of the previous two,
            // it must be the repeated element
            if (nums[i - 2] == nums[i] || nums[i - 1] == nums[i]) {
                return nums[i];
            }
        }

        // Fallback case: repeated element must be at the end
        return nums[nums.size() - 1];
    }
};
```

## Test Cases Analysis

| Input             | Output |
| ----------------- | ------ |
| [1,2,3,3]         | 3      |
| [2,1,2,5,3,2]     | 2      |
| [5,1,5,2,5,3,5,4] | 5      |
| [9,9,1,2]         | 9      |

## Edge Cases to Consider

* Repeated element appears at the start
* Repeated element appears at the end
* Minimal array size (`2N = 2`)

## Common Test Cases

* Repeated element clustered together
* Repeated element evenly spaced
* Random order arrays

## Common Mistakes to Avoid

* Assuming the repeated element must be adjacent
* Using sorting unnecessarily
* Forgetting problem guarantees

## Interview Relevance

* Frequently asked array problem
* Demonstrates problem constraint exploitation
* Highlights space-time tradeoffs

## What This Problem Teaches

* Leveraging problem guarantees
* Identifying hidden patterns in constraints
* Choosing optimal data structures

## Key Takeaways

* Constraints often imply stronger guarantees than stated
* O(1) space solutions are sometimes hidden in observations
* Early exits improve performance and clarity

## Problem Difficulty Analysis

This is an **Easy-level** problem.
While the brute-force approach is straightforward, the optimal constant-space solution demonstrates deeper reasoning and is often discussed in interviews.
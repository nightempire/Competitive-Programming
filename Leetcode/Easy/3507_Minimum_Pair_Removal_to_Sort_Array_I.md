# Minimum Pair Removal to Sort Array I

## Platform

LeetCode

## Problem Link

[3507. Minimum Pair Removal to Sort Array I](https://leetcode.com/problems/minimum-pair-removal-to-sort-array-i/)

## Problem Statement

You are given an integer array `nums`.

In one operation, you may:

* Choose **two adjacent elements**
* Remove them
* Insert their **sum** back into the array at the same position

The array size is reduced by one after each operation.

Your task is to determine the **minimum number of such operations** required to make the array **non-decreasing** (sorted in ascending order).

## Input Format

* An integer array `nums`

## Output Format

* A single integer representing the minimum number of operations required to make the array sorted

## Constraints

* `1 ≤ nums.length ≤ 100`
* `-10^9 ≤ nums[i] ≤ 10^9`

## Examples

### Example 1

Input

```
nums = [5, 2, 3, 1]
```

Explanation

* The array is not sorted
* Adjacent pair sums:

  * (5, 2) → 7
  * (2, 3) → 5
  * (3, 1) → 4 ← minimum
* Remove `3` and `1`, insert `4` → `[5, 2, 4]`
* Still not sorted
* Next minimum adjacent sum: `(2, 4) → 6`
* Array becomes `[5, 6]`
* Sorted

Total operations:

```
2
```

### Example 2

Input

```
nums = [1, 2, 3, 4]
```

Explanation

* Array is already sorted

Output

```
0
```

## Approach

**Greedy Simulation with Repeated Pair Merging**

## Intuition

To make the array sorted using the fewest operations:

* We want to **merge elements that least disrupt order**
* Merging the **adjacent pair with the smallest sum** minimizes the chance of creating a large out-of-order value
* Repeating this process gradually smooths the array into a non-decreasing sequence

At each step:

* Check if the array is already sorted
* If not, perform one optimal merge and continue

## Algorithm Steps

* Initialize an operation counter
* While the array is not sorted:

  * Increment the operation counter
  * Find the adjacent pair with the **minimum sum**
  * Replace the pair with their sum
  * Reduce the array size by one
* Return the operation counter

## Visual Walkthrough

### Case 1

Initial array:

```
[5, 2, 3, 1]
```

Minimum adjacent sum:

```
3 + 1 = 4
```

After merge:

```
[5, 2, 4]
```

---

Next step:

Minimum adjacent sum:

```
2 + 4 = 6
```

After merge:

```
[5, 6]
```

Array is now sorted.

Total operations:

```
2
```

---

### Case 2

Initial array:

```
[1, 2, 3, 4]
```

Already sorted.

Operations:

```
0
```

## Complexity Analysis

### Time Complexity

**O(n²)**

* Each operation checks whether the array is sorted → O(n)
* Finding the minimum adjacent sum → O(n)
* In the worst case, up to `n − 1` operations are required

### Space Complexity

**O(1)**

* The array is modified in place
* Only constant extra variables are used

## Solution Explanation

The solution simulates the process exactly as defined in the problem.
At every step, it greedily selects the adjacent pair with the smallest sum, ensuring minimal impact on ordering. By repeatedly merging such pairs and checking for sortedness, the algorithm guarantees the minimum number of operations required.

## Full Solution

### C++ Implementation

```cpp
class Solution {
public:
    int minimumPairRemoval(vector<int>& nums) {

        // Current size of the array
        int n = nums.size();

        // Counter to track number of operations performed
        int operations = 0;

        // Repeat until the array becomes non-decreasing
        while (true) {

            // Check if the array is already sorted
            bool isSorted = true;
            for (int i = 1; i < n; i++) {
                if (nums[i - 1] > nums[i]) {
                    isSorted = false;
                    break;
                }
            }

            // If sorted, stop the process
            if (isSorted) {
                break;
            }

            // One operation will be performed
            operations++;

            // Find the adjacent pair with the minimum sum
            int minSum = INT_MAX;
            int minIndex = -1;

            for (int i = 1; i < n; i++) {
                int currentSum = nums[i - 1] + nums[i];
                if (currentSum < minSum) {
                    minSum = currentSum;
                    minIndex = i - 1;
                }
            }

            // Replace the selected pair with their sum
            nums[minIndex] = minSum;

            // Shift elements left to remove one position
            for (int i = minIndex + 1; i < n - 1; i++) {
                nums[i] = nums[i + 1];
            }

            // Reduce array size
            n--;
        }

        // Return total number of operations
        return operations;
    }
};
```

## Test Cases Analysis

| Input Array    | Output | Reasoning                            |
| -------------- | ------ | ------------------------------------ |
| `[1, 2, 3, 4]` | 0      | Already sorted                       |
| `[5, 2, 3, 1]` | 2      | Two optimal merges required          |
| `[3, 1]`       | 1      | Single merge results in sorted array |
| `[4, 3, 2, 1]` | 3      | Gradual merges until sorted          |

## Edge Cases to Consider

* Array of length 1
* Array of length 2
* Already sorted array
* Arrays with negative values
* Arrays with large integer values

## Common Test Cases

* Reverse sorted arrays
* Nearly sorted arrays
* Arrays with repeated values

## Common Mistakes to Avoid

* Forgetting to re-check sortedness after each merge
* Incorrectly shifting elements after merging
* Not updating the effective array size

## Interview Relevance

* Tests greedy decision-making
* Evaluates simulation and array manipulation skills
* Common pattern in array transformation problems

## What This Problem Teaches

* How greedy choices can lead to optimal solutions
* Managing dynamic array size during simulation
* Importance of step-by-step validation

## Key Takeaways

* Always minimize disruption when modifying arrays
* Greedy local decisions can produce global optimal results
* Simulation problems require careful boundary handling

## Problem Difficulty Analysis

This is an **Medium-level** problem.
While the logic is straightforward, careful implementation and repeated validation make it more challenging than basic array problems.
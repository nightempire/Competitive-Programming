# B_Honest_Coach

## Platform

Codeforces

## Problem Link

[B. Honest Coach](https://codeforces.com/problemset/problem/1360/B)

## Problem Statement

You are given multiple test cases.
In each test case, you are given an integer `n` representing the number of athletes, followed by `n` integers representing their strengths.

The coach wants to select **two athletes** such that the **absolute difference between their strengths is minimized**.

Your task is to compute and output the **minimum possible difference** between the strengths of any two athletes.

Each test case is independent.

## Input Format

* The first line contains an integer `t`, the number of test cases.
* For each test case:

  * The first line contains an integer `n`, the number of athletes.
  * The second line contains `n` integers representing the strengths.

## Output Format

For each test case, print a single integer — the **minimum difference** between the strengths of any two athletes.

Each answer should be printed on a new line.

## Constraints

* `1 ≤ t ≤ 1000`
* `2 ≤ n ≤ 50`
* `1 ≤ strength ≤ 1000`

## Examples

### Example 1

Input

```
2
4
1 6 9 3
3
10 20 30
```

Explanation

* Test case 1:

  * Sorted strengths → `[1, 3, 6, 9]`
  * Differences → `2, 3, 3`
  * Minimum difference → `2`
* Test case 2:

  * Differences → `10, 10`
  * Minimum difference → `10`

Output

```
2
10
```

### Example 2

Input

```
1
5
5 5 5 5 5
```

Explanation

* All athletes have equal strength
* Minimum difference → `0`

Output

```
0
```

## Approach

**Sorting followed by adjacent difference comparison**

## Intuition

If the strengths are sorted:

* The minimum difference between any two elements **must occur between two adjacent elements**.

There is no need to check every possible pair.
Sorting simplifies the problem and ensures an efficient comparison strategy.

## Algorithm Steps

* Read integer `t`
* For each test case:

  * Read integer `n`
  * Read the `n` strengths into an array
  * Sort the array
  * Initialize a variable to track the minimum difference
  * Compare differences of adjacent elements
  * Output the smallest difference found

## Visual Walkthrough

### Test Case 1

Input:

```
1 6 9 3
```

After sorting:

```
[1, 3, 6, 9]
```

Differences:

```
3 - 1 = 2
6 - 3 = 3
9 - 6 = 3
```

Minimum difference:

```
2
```

---

### Test Case 2

Input:

```
7 7 7
```

After sorting:

```
[7, 7, 7]
```

Differences:

```
0, 0
```

Minimum difference:

```
0
```

---

### Test Case 3

Input:

```
2 1000
```

After sorting:

```
[2, 1000]
```

Difference:

```
998
```

Result:

```
998
```

## Complexity Analysis

### Time Complexity

**O(n log n)**

Sorting the array dominates the time complexity.
The subsequent traversal is linear.

### Space Complexity

**O(1)** (excluding input storage)

Only a constant amount of extra space is used.

## Solution Explanation

The solution sorts the array of strengths to bring similar values closer together.
It then iterates through the sorted list, computing differences between consecutive elements and tracking the minimum.

This guarantees correctness because any non-adjacent pair would have a difference greater than or equal to one of the adjacent differences.

## Full Solution

### C++ Implementation

```cpp
#include <iostream>
#include <algorithm>
using namespace std;

int main() {

    // Number of test cases
    int t;
    cin >> t;

    while (t--) {

        // Number of athletes
        int n;
        cin >> n;

        // Array to store strengths
        int nums[n];

        // Variable to store the minimum difference
        int mini = 1000;

        // Read strengths
        for (int i = 0; i < n; i++) {
            cin >> nums[i];
        }

        // Sort the strengths
        sort(nums, nums + n);

        // Compare adjacent elements
        for (int i = 1; i < n; i++) {
            mini = min(mini, nums[i] - nums[i - 1]);
        }

        // Output the result
        cout << mini << '\n';
    }

    return 0;
}
```

## Test Cases Analysis

| Test Case | Strengths | Sorted Order | Minimum Difference |
| --------- | --------- | ------------ | ------------------ |
| 1         | 1 6 9 3   | 1 3 6 9      | 2                  |
| 2         | 10 20 30  | 10 20 30     | 10                 |
| 3         | 5 5 5 5 5 | 5 5 5 5 5    | 0                  |
| 4         | 2 1000    | 2 1000       | 998                |

## Edge Cases to Consider

* All strengths are equal
* Minimum possible `n = 2`
* Strength values at extreme limits

## Common Test Cases

* Random strengths
* Already sorted input
* Reverse sorted input

## Common Mistakes to Avoid

* Checking all pairs unnecessarily
* Forgetting to sort before comparison
* Incorrect initialization of the minimum value

## Interview Relevance

* Demonstrates sorting-based optimization
* Tests understanding of pairwise differences
* Common greedy-style reasoning problem

## What This Problem Teaches

* Sorting can drastically simplify problems
* Adjacent comparisons are often sufficient
* Brute force is not always necessary

## Key Takeaways

* Always consider sorting when minimizing differences
* Efficient logic improves clarity and performance
* Small constraints still benefit from clean solutions

## Problem Difficulty Analysis

This is an **Easy-level** problem.
It focuses on observation and efficient use of sorting rather than complex algorithms.
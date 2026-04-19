## 1933A. Turtle Puzzle: Rearrange and Negate

## Platform

Codeforces

## Problem Link

[Turtle Puzzle: Rearrange and Negate](https://codeforces.com/problemset/problem/1933/A)

## Problem Statement

You are given an array of integers. You are allowed to perform the following operations any number of times:

* Rearrange the elements of the array in any order.
* Choose any element and negate it (i.e., multiply it by `-1`).

Your task is to determine the **maximum possible sum** of the array after performing these operations optimally.

## Input Format

* The first line contains an integer `t`, the number of test cases.
* For each test case:

  * The first line contains an integer `n`, the size of the array.
  * The second line contains `n` integers representing the array elements.

## Output Format

* For each test case, print a single integer — the maximum possible sum of the array.

## Constraints

* `1 ≤ t ≤ 10^4`
* `1 ≤ n ≤ 2 × 10^5`
* `-10^9 ≤ a[i] ≤ 10^9`
* The sum of all `n` across test cases does not exceed `2 × 10^5`

## Examples

### Example 1

Input

```
1
5
-1 -2 -3 4 5
```

Explanation

Convert all negative numbers to positive:

```
1 + 2 + 3 + 4 + 5 = 15
```

Output

```
15
```

---

### Example 2

Input

```
1
3
0 -7 2
```

Explanation

```
0 + 7 + 2 = 9
```

Output

```
9
```

---

### Example 3

Input

```
1
4
-10 -20 -30 -40
```

Explanation

All values can be negated:

```
10 + 20 + 30 + 40 = 100
```

Output

```
100
```

## Approach

Greedy Approach (Absolute Value Maximization)

## Intuition

Since you can:

* Rearrange elements freely
* Negate any element any number of times

There is **no restriction** preventing you from making every element non-negative.

Thus, the best strategy is:

* Convert all elements to their absolute values
* Sum them up

This guarantees the maximum possible sum.

## Algorithm Steps

* Read number of test cases `t`
* For each test case:

  * Read `n`
  * Initialize `sum = 0`
  * Loop through all elements:

    * Convert each element to its absolute value
    * Add it to `sum`
  * Output `sum`

## Visual Walkthrough

### Case 1

```
Array: [-1, -2, 3]
```

```
Step 1: Convert → [1, 2, 3]
Step 2: Sum → 6
```

---

### Case 2

```
Array: [4, -5, -6]
```

```
Step 1: Convert → [4, 5, 6]
Step 2: Sum → 15
```

---

### Case 3

```
Array: [0, -1, 2]
```

```
Step 1: Convert → [0, 1, 2]
Step 2: Sum → 3
```

## Complexity Analysis

### Time Complexity

**O(n) per test case**

Each element is processed exactly once.

### Space Complexity

**O(1)**

No extra space is used apart from variables.

## Solution Explanation

The solution leverages the fact that negating any number is always allowed. Therefore, each negative number can be flipped to positive. Rearranging has no effect on the sum, so the optimal solution is simply the sum of absolute values of all elements.

## Full Solution

### C++ Implementation

```cpp
#include<iostream>
using namespace std;

int main() {

    // Number of test cases
    int t;
    cin >> t;

    // Process each test case
    while(t--) {

        // Number of elements
        int n;

        // Variable to store final sum
        int sum = 0;

        cin >> n;

        // Process all elements
        while(n--) {

            int num;
            cin >> num;

            // Convert negative numbers to positive
            // and add to sum
            sum += (num < 0 ? -num : num);
        }

        // Output the result
        cout << sum << '\n';
    }

    return 0;
}
```

## Test Cases Analysis

| Input Array     | Converted Array | Output |
| --------------- | --------------- | ------ |
| [-1, -2, -3]    | [1, 2, 3]       | 6      |
| [0, -7, 2]      | [0, 7, 2]       | 9      |
| [5, 6, 7]       | [5, 6, 7]       | 18     |
| [-10, -20, -30] | [10, 20, 30]    | 60     |

## Edge Cases to Consider

* All elements are zero
* All elements are negative
* Single element array
* Large values (check integer overflow)

## Common Test Cases

* Mixed positive and negative numbers
* Only positive numbers
* Only negative numbers
* Arrays containing zero

## Common Mistakes to Avoid

* Forgetting to reset `sum` for each test case
* Using incorrect absolute value logic
* Integer overflow if constraints are large

## Interview Relevance

* Tests greedy reasoning
* Evaluates understanding of problem constraints
* Focuses on optimization through observation

## What This Problem Teaches

* Importance of identifying unrestricted operations
* Simplifying problems using mathematical properties
* Efficient single-pass solutions

## Key Takeaways

* When negation is unrestricted, absolute values maximize sum
* Rearrangement does not affect total sum
* Always look for simplifications before complex logic

## Problem Difficulty Analysis

This is an **Easy-level** problem.

The main challenge lies in recognizing that all elements can be made non-negative, leading to a direct and optimal solution.
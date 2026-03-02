# A_Ambitious_Kid

## Platform

Codeforces

## Problem Link

[A. Ambitious Kid](https://codeforces.com/problemset/problem/1866/A)

## Problem Statement

An ambitious kid wants to achieve the smallest possible absolute score from a list of integers.

You are given `n` integers. Your task is to determine the **minimum absolute value** among them.

In other words, find the number in the list whose absolute value is the smallest and print that absolute value.

## Input Format

* The first line contains an integer `n` — the number of integers.
* The second line contains `n` integers.

## Output Format

Print a single integer — the minimum absolute value among the given numbers.

## Constraints

* `1 ≤ n ≤ 100`
* `-100 ≤ ai ≤ 100`

## Examples

### Example 1

Input

```
5
-2 4 3 -1 5
```

Explanation

Absolute values:

```
2 4 3 1 5
```

Minimum absolute value = `1`

Output

```
1
```

---

### Example 2

Input

```
3
7 -9 4
```

Explanation

Absolute values:

```
7 9 4
```

Minimum absolute value = `4`

Output

```
4
```

---

### Example 3

Input

```
4
0 -3 8 -6
```

Explanation

Absolute values:

```
0 3 8 6
```

Minimum absolute value = `0`

Output

```
0
```

## Approach

Linear Scan (Single Pass Minimum Tracking)

## Intuition

The problem requires identifying the smallest absolute value among given integers.

Instead of storing all values or sorting them, we can:

* Convert each number to its absolute value.
* Maintain a running minimum.
* Update the minimum whenever a smaller absolute value is encountered.

Since each number is processed once, this guarantees efficiency and simplicity.

## Algorithm Steps

* Read integer `n`.
* Initialize a variable `mn` with a very large value.
* For each of the `n` integers:

  * Read the number.
  * Compute its absolute value.
  * Update `mn = min(mn, abs(number))`.
* Print `mn`.

## Visual Walkthrough

Consider the input:

```
5
-2 4 3 -1 5
```

Step-by-step execution:

Initial:

```
mn = ∞
```

Processing elements:

| Element | Absolute Value | Current Minimum |
| ------- | -------------- | --------------- |
| -2      | 2              | 2               |
| 4       | 4              | 2               |
| 3       | 3              | 2               |
| -1      | 1              | 1               |
| 5       | 5              | 1               |

Final answer:

```
1
```

---

Another example:

```
4
0 -3 8 -6
```

Processing:

| Element | Absolute Value | Current Minimum |
| ------- | -------------- | --------------- |
| 0       | 0              | 0               |
| -3      | 3              | 0               |
| 8       | 8              | 0               |
| -6      | 6              | 0               |

Final answer:

```
0
```

## Complexity Analysis

### Time Complexity

O(n)

Each element is processed exactly once.
There are no nested loops or additional passes.

### Space Complexity

O(1)

Only a few integer variables are used regardless of input size.

## Solution Explanation

The solution maintains a running minimum of absolute values while iterating through the list.

By using `abs()` for each number and updating the minimum accordingly, we efficiently compute the required result in a single pass.

No additional data structures are required, making the solution optimal in both time and space.

## Full Solution

### C++ Implementation

```cpp
#include <iostream>
#include <climits>   // For INT_MAX
#include <cmath>     // For abs()

using namespace std;

int main() {

    // Variable to store number of integers
    int n;

    // Variable to track the minimum absolute value
    int mn = INT_MAX;

    // Read the number of elements
    cin >> n;

    // Loop through all elements
    for (int i = 0; i < n; i++) {

        // Read each number
        int num;
        cin >> num;

        // Update minimum with the absolute value
        // abs(num) ensures negative numbers are handled correctly
        mn = min(mn, abs(num));
    }

    // Output the minimum absolute value found
    cout << mn;

    return 0;
}
```

## Test Cases Analysis

| Test Case | Input            | Absolute Values | Output |
| --------- | ---------------- | --------------- | ------ |
| 1         | 1<br>5           | 5               | 5      |
| 2         | 3<br>7 -9 4      | 7 9 4           | 4      |
| 3         | 4<br>0 -3 8 -6   | 0 3 8 6         | 0      |
| 4         | 5<br>-2 4 3 -1 5 | 2 4 3 1 5       | 1      |

## Edge Cases to Consider

* `n = 1`
* All numbers are positive
* All numbers are negative
* Presence of `0`
* All values having same absolute value

## Common Test Cases

* Mixed positive and negative integers
* Single element input
* Input containing zero
* Maximum constraint values

## Common Mistakes to Avoid

* Forgetting to use `abs()` before comparison
* Initializing minimum as `0` instead of a large value
* Not including `<climits>` for `INT_MAX`

## Interview Relevance

* Tests understanding of absolute values
* Demonstrates basic iteration and minimum tracking
* Common warm-up or screening-level problem

## What This Problem Teaches

* Efficient single-pass scanning
* Handling negative numbers correctly
* Writing clean and optimized logic for simple tasks

## Key Takeaways

* Always consider absolute value when sign is irrelevant
* Use proper initialization for tracking minimum
* Linear scan is often sufficient for simple comparison problems

## Problem Difficulty Analysis

This is an **Easy-level** problem.

It focuses on fundamental programming concepts such as loops, conditionals, and mathematical functions. It is ideal for beginners and for practicing clean implementation of simple logic.
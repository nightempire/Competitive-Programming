# A. Restoring Three Numbers

## Platform

Codeforces

## Problem Link

[A. Restoring Three Numbers](https://codeforces.com/problemset/problem/1154/A)

## Problem Statement

You are given **four integers**.
These integers represent the values:

```
a + b
a + c
b + c
a + b + c
```

in some order.

Your task is to **restore the original three numbers** `a`, `b`, and `c`.

## Input Format

* A single line containing four integers.

## Output Format

Print three integers representing the values of `a`, `b`, and `c`.

The order of output does not matter.

## Constraints

* `1 ≤ value ≤ 10^9`
* All values fit within 32-bit integers.

## Examples

### Example 1

Input

```
2 3 4 5
```

Explanation

The maximum value is:

```
a + b + c = 5
```

Then:

```
a = 5 - (b + c) = 1
b = 5 - (a + c) = 2
c = 5 - (a + b) = 3
```

Output

```
1 2 3
```

### Example 2

Input

```
10 7 6 3
```

Explanation

Maximum value:

```
a + b + c = 10
```

Remaining values:

```
7, 6, 3
```

Restored numbers:

```
3 4 7
```

### Example 3

Input

```
100 100 100 200
```

Explanation
All pair sums are equal.

Output

```
100 100 100
```

## Approach

**Mathematical Deduction Using Maximum Value**

## Intuition

Among the four given numbers, the **largest value must be `a + b + c`**.
Each of the remaining three values is missing exactly one of the numbers.

So:

```
a = (a + b + c) − (b + c)
b = (a + b + c) − (a + c)
c = (a + b + c) − (a + b)
```

This observation allows direct reconstruction.

## Algorithm Steps

* Read the four integers
* Identify the maximum value
* Subtract each of the other three values from the maximum
* Output the results

## Visual Walkthrough

Input:

```
2 3 4 5
```

Identify:

```
max = 5
```

Compute:

```
5 − 2 = 3
5 − 3 = 2
5 − 4 = 1
```

Restored numbers:

```
1 2 3
```

Another case:

```
3 6 7 10
```

```
10 − 3 = 7
10 − 6 = 4
10 − 7 = 3
```

## Complexity Analysis

### Time Complexity

O(1)

Only four elements are processed.

### Space Complexity

O(1)

Uses a fixed-size array.

## Solution Explanation

The solution relies on identifying the total sum `a + b + c` and subtracting the remaining values to retrieve the original numbers. This avoids sorting or complex logic and directly applies mathematical reasoning.

## Full Solution

### C++ Implementation

```cpp
#include <iostream>
using namespace std;

int main() {

    // Array to store the four given numbers
    int nums[4];

    // Variable to track the maximum value
    int maxi = 0;

    // Read input and find the maximum value
    for (int i = 0; i < 4; i++) {
        cin >> nums[i];
        if (nums[i] > maxi) {
            maxi = nums[i];
        }
    }

    // The maximum value represents a + b + c
    // Subtract each remaining value from it
    for (int i = 0; i < 4; i++) {
        if (nums[i] != maxi) {
            cout << maxi - nums[i] << " ";
        }
    }

    return 0;
}
```

## Test Cases Analysis

| Input Values    | Restored Numbers |
| --------------- | ---------------- |
| 2 3 4 5         | 1 2 3            |
| 10 7 6 3        | 3 4 7            |
| 100 100 100 200 | 100 100 100      |
| 1 1 1 3         | 2 2 2            |

## Edge Cases to Consider

* All three original numbers are equal
* Very large input values
* Inputs already in sorted or unsorted order

## Common Test Cases

* Distinct values
* Duplicate pair sums
* Symmetric inputs

## Common Mistakes to Avoid

* Sorting unnecessarily
* Forgetting to identify the maximum correctly
* Printing the maximum difference instead of individual values

## Interview Relevance

* Tests mathematical deduction skills
* Evaluates observation-based problem solving
* Common example of reverse engineering values

## What This Problem Teaches

* Using mathematical properties to simplify problems
* Avoiding brute-force approaches
* Importance of identifying key values

## Key Takeaways

* Maximum value often carries critical information
* Simple arithmetic can replace complex logic
* Observations can lead to constant-time solutions

## Problem Difficulty Analysis

This is an **Easy-level** problem.
It emphasizes logical reasoning and arithmetic clarity rather than algorithmic complexity, making it suitable for beginners and technical interview preparation.

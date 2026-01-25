# A. My First Sorting Problem

## Platform

Codeforces

## Problem Link

[A. My First Sorting Problem](https://codeforces.com/problemset/problem/1551/A)

## Problem Statement

You are given multiple test cases.
For each test case, two integers `a` and `b` are provided.

Your task is to output the two integers in **non-decreasing (sorted) order**.

This problem introduces the fundamental concept of sorting using simple comparisons.

## Input Format

* The first line contains an integer `t`, the number of test cases.
* Each of the next `t` lines contains two integers `a` and `b`.

## Output Format

For each test case, print two integers in sorted order (`min max`) on a single line.

## Constraints

* `1 ≤ t ≤ 1000`
* `0 ≤ a, b ≤ 1000`

## Examples

### Example 1

Input

```
3
1 2
10 5
7 7
```

Explanation

* Test case 1: `1 2` is already sorted
* Test case 2: `10 5` → sorted as `5 10`
* Test case 3: Both values are equal

Output

```
1 2
5 10
7 7
```

### Example 2

Input

```
1
100 1
```

Explanation

The smaller number should be printed first.

Output

```
1 100
```

## Approach

Direct comparison and conditional swapping.

## Intuition

Since only **two numbers** are involved per test case, a full sorting algorithm is unnecessary.
A simple comparison followed by a swap (if needed) ensures the numbers are printed in sorted order.

This keeps the solution minimal and efficient.

## Algorithm Steps

* Read the number of test cases `t`.
* For each test case:

  * Read integers `a` and `b`.
  * If `a` is greater than `b`, swap them.
  * Print `a` followed by `b`.

## Visual Walkthrough

### Test Case 1

Input:

```
a = 10, b = 5
```

Comparison:

```
10 > 5 → swap
```

After swap:

```
5 10
```

---

### Test Case 2

Input:

```
a = 3, b = 7
```

Comparison:

```
3 < 7 → no swap needed
```

Output:

```
3 7
```

---

### Test Case 3

Input:

```
a = 6, b = 6
```

Comparison:

```
6 == 6 → already sorted
```

Output:

```
6 6
```

## Complexity Analysis

### Time Complexity

O(t)

Each test case performs a constant-time comparison.

### Space Complexity

O(1)

Only a few integer variables are used.

## Solution Explanation

The solution processes each test case independently.
By comparing the two numbers and swapping them when necessary, it guarantees sorted output.

This approach is optimal given the problem’s simplicity and constraints.

## Full Solution

### C++ Implementation

```cpp
#include <iostream>
using namespace std;

int main() {

    // Number of test cases
    int t;
    cin >> t;

    // Process each test case
    while (t--) {

        // Read the two integers
        int a, b;
        cin >> a >> b;

        // If a is greater than b, swap them
        if (a > b) {
            int temp = a;
            a = b;
            b = temp;
        }

        // Output the sorted pair
        cout << a << " " << b << '\n';
    }

    return 0;
}
```

## Test Cases Analysis

| Input (a, b) | Output | Reason          |
| ------------ | ------ | --------------- |
| 1 2          | 1 2    | Already sorted  |
| 10 5         | 5 10   | Swap required   |
| 7 7          | 7 7    | Equal values    |
| 0 100        | 0 100  | Boundary values |

## Edge Cases to Consider

* Both numbers are equal
* One or both numbers are zero
* Maximum constraint values

## Common Test Cases

* Small integers
* Reversed order inputs
* Identical numbers

## Common Mistakes to Avoid

* Forgetting to swap values
* Printing in the wrong order
* Using unnecessary sorting logic

## Interview Relevance

* Tests basic comparison logic
* Introduces conditional swapping
* Common beginner-level interview problem

## What This Problem Teaches

* Fundamental sorting principles
* Efficient problem-solving for small inputs
* Importance of minimal logic

## Key Takeaways

* Simple problems require simple solutions
* Avoid overengineering
* Always match logic to constraints

## Problem Difficulty Analysis

This is an **Easy-level** problem.
It serves as an introductory exercise for beginners learning conditional statements and sorting basics.
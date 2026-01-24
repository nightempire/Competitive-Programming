# A. Easy Problem

## Platform

Codeforces

## Problem Link

[A. Easy Problem](https://codeforces.com/problemset/problem/1760/A)

## Problem Statement

You are given an integer `t`, representing the number of test cases.
For each test case, you are given an integer `n`.

For every test case, output the value of `n - 1`.

This problem focuses on handling multiple test cases and performing a simple arithmetic operation for each case.

## Input Format

* The first line contains a single integer `t`, the number of test cases.
* The next `t` lines each contain a single integer `n`.

## Output Format

For each test case, print a single integer — the result of `n - 1` — on a new line.

## Constraints

* `1 ≤ t ≤ 10^4`
* `1 ≤ n ≤ 10^9`

## Examples

### Example 1

Input

```
3
5
1
10
```

Explanation

* Test case 1: `5 - 1 = 4`
* Test case 2: `1 - 1 = 0`
* Test case 3: `10 - 1 = 9`

Output

```
4
0
9
```

### Example 2

Input

```
1
100
```

Explanation

* `100 - 1 = 99`

Output

```
99
```

## Approach

Constant-time arithmetic computation per test case.

## Intuition

The problem does not require any conditional logic or iteration over values inside a test case.
For every given integer `n`, the required output is simply one less than `n`.

Since each test case is independent, the same operation is applied repeatedly.

## Algorithm Steps

* Read the integer `t`.
* Repeat the following steps `t` times:

  * Read the integer `n`.
  * Compute `n - 1`.
  * Print the result.

## Visual Walkthrough

Consider the following test cases:

Input:

```
n = 5
```

Computation:

```
5 - 1 = 4
```

---

Input:

```
n = 1
```

Computation:

```
1 - 1 = 0
```

---

Input:

```
n = 10
```

Computation:

```
10 - 1 = 9
```

Each test case applies the same direct subtraction.

## Complexity Analysis

### Time Complexity

O(t)

Each test case requires a constant-time subtraction operation.

### Space Complexity

O(1)

Only a few integer variables are used regardless of input size.

## Solution Explanation

The program reads the number of test cases and processes each independently.
For every input integer `n`, it directly prints `n - 1`.

This approach is optimal, minimal, and fully aligned with the problem requirements.

## Full Solution

### C++ Implementation

```cpp
#include <iostream>
using namespace std;

int main() {

    // Read the number of test cases
    int t;
    cin >> t;

    // Process each test case
    while (t--) {

        // Read the integer n for the current test case
        int n;
        cin >> n;

        // Output n - 1 as required by the problem
        cout << n - 1 << '\n';
    }

    return 0;
}
```

## Test Cases Analysis

| Test Case | Input `n` | Output | Reasoning            |
| --------- | --------- | ------ | -------------------- |
| 1         | 1         | 0      | Minimum valid value  |
| 2         | 2         | 1      | Simple subtraction   |
| 3         | 10        | 9      | Standard case        |
| 4         | 1000000   | 999999 | Large input handling |

## Edge Cases to Consider

* `n = 1`, where the output becomes `0`
* Maximum constraint values
* Single test case input

## Common Test Cases

* Small integers
* Large integers
* Multiple test cases with mixed values

## Common Mistakes to Avoid

* Forgetting to process multiple test cases
* Printing extra spaces or lines
* Misreading input order

## Interview Relevance

* Tests basic input-output handling
* Evaluates understanding of test case loops
* Common warm-up problem in coding interviews

## What This Problem Teaches

* Efficient handling of multiple test cases
* Importance of understanding problem simplicity
* Writing clean and minimal code

## Key Takeaways

* Not every problem requires complex logic
* Direct mapping from problem statement to code is often optimal
* Accuracy in input handling is essential

## Problem Difficulty Analysis

This is an **Easy-level** problem.
It focuses on foundational programming skills and is ideal for beginners or as a quick confidence-building exercise.
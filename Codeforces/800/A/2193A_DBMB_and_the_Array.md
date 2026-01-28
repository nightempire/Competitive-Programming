# A. DBMB and the Array

## Platform

Codeforces

## Problem Link

[A. DBMB and the Array](https://codeforces.com/problemset/problem/2193/A)

## Problem Statement

You are given an array of integers and two additional integers `s` and `x`.

You may **add the value `x` any number of times** to the array elements (including zero times).

Your task is to determine whether it is possible to make the **sum of the array exactly equal to `s`** after performing the allowed operations.

For each test case, output `"YES"` if it is possible to achieve the target sum, otherwise output `"NO"`.

## Input Format

* The first line contains an integer `t`, the number of test cases.
* For each test case:

  * A single line containing three integers `n`, `s`, and `x`.
  * A single line containing `n` integers representing the array elements.

## Output Format

For each test case, print `"YES"` if the target sum `s` can be achieved, otherwise print `"NO"`.

## Constraints

* `1 ≤ t ≤ 10⁴`
* `1 ≤ n ≤ 100`
* `0 ≤ ai ≤ 10⁹`
* `0 ≤ s, x ≤ 10⁹`

## Examples

### Example 1

Input

```
1
3 10 2
2 3 3
```

Explanation

Initial sum of the array:

```
2 + 3 + 3 = 8
```

Difference needed:

```
10 − 8 = 2
```

Since `2` is divisible by `x = 2`, the target sum can be achieved.

Output

```
YES
```

### Example 2

Input

```
1
4 7 3
1 1 1 1
```

Explanation

Initial sum:

```
1 + 1 + 1 + 1 = 4
```

Difference needed:

```
7 − 4 = 3
```

Since `3` is divisible by `x = 3`, the target sum can be achieved.

Output

```
YES
```

### Example 3

Input

```
1
2 5 4
1 1
```

Explanation

Initial sum:

```
1 + 1 = 2
```

Difference needed:

```
5 − 2 = 3
```

Since `3` is **not divisible** by `x = 4`, the target sum cannot be achieved.

Output

```
NO
```

## Approach

**Greedy arithmetic feasibility check**

## Intuition

The array’s sum can only be increased in **steps of size `x`**.

Therefore:

* If the current sum already exceeds `s`, it is impossible.
* Otherwise, the difference `(s − current_sum)` must be divisible by `x`.

If both conditions hold, the target sum is achievable.

## Algorithm Steps

* Read the number of test cases.
* For each test case:

  * Read `n`, `s`, and `x`.
  * Compute the sum of all array elements.
  * If the sum is greater than `s`, print `"NO"`.
  * Otherwise, check whether `(s − sum)` is divisible by `x`.

    * If yes, print `"YES"`.
    * Otherwise, print `"NO"`.

## Visual Walkthrough

### Case 1

Array: `[2, 3, 3]`, `s = 10`, `x = 2`

```
Current sum = 8
Needed = 10 − 8 = 2
2 % 2 = 0 → Valid
```

### Case 2

Array: `[1, 1]`, `s = 5`, `x = 4`

```
Current sum = 2
Needed = 5 − 2 = 3
3 % 4 ≠ 0 → Invalid
```

### Case 3

Array: `[5, 5]`, `s = 6`

```
Current sum = 10
10 > 6 → Invalid
```

## Complexity Analysis

### Time Complexity

**O(n) per test case**

Each array element is read and added once.

### Space Complexity

**O(1)**

Only a few integer variables are used regardless of input size.

## Solution Explanation

The solution computes the total sum of the array and determines whether the remaining value required to reach `s` can be constructed using repeated additions of `x`.

This avoids unnecessary simulation and directly checks mathematical feasibility, making the solution optimal and efficient.

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

        // n -> number of elements
        // s -> target sum
        // x -> value that can be added repeatedly
        int n, s, x;
        cin >> n >> s >> x;

        // Variable to store sum of array elements
        int sum = 0;

        // Read array elements and calculate sum
        for (int i = 0; i < n; i++) {
            int num;
            cin >> num;
            sum += num;
        }

        // If current sum already exceeds target,
        // it is impossible to reduce it
        if (sum > s) {
            cout << "NO\n";
        }
        // Otherwise, check if the difference
        // can be formed using multiples of x
        else if ((s - sum) % x != 0) {
            cout << "NO\n";
        }
        // Valid case
        else {
            cout << "YES\n";
        }
    }

    return 0;
}
```

## Test Cases Analysis

| Test Case | Array Sum | Target `s` | `x` | Result | Reason                      |
| --------- | --------- | ---------- | --- | ------ | --------------------------- |
| `[2,3,3]` | 8         | 10         | 2   | YES    | Difference divisible by `x` |
| `[1,1]`   | 2         | 5          | 4   | NO     | Difference not divisible    |
| `[5,5]`   | 10        | 6          | 1   | NO     | Sum already exceeds `s`     |
| `[1,1,1]` | 3         | 3          | 5   | YES    | No additions needed         |

## Edge Cases to Consider

* Initial sum equal to `s`
* Initial sum greater than `s`
* `x = 0`
* Single-element array

## Common Test Cases

* Small arrays with exact match
* Large arrays with excess sum
* Difference exactly equal to `x`

## Common Mistakes to Avoid

* Forgetting to handle `sum > s`
* Using floating-point division instead of modulo
* Assuming at least one operation is mandatory

## Interview Relevance

* Tests mathematical reasoning
* Evaluates edge-case handling
* Reinforces modular arithmetic concepts

## What This Problem Teaches

* Reducing problems to arithmetic feasibility
* Avoiding brute-force simulation
* Writing clean conditional logic

## Key Takeaways

* Always check feasibility before simulation
* Modular arithmetic simplifies repeated operations
* Greedy checks can replace loops

## Problem Difficulty Analysis

This is an **Easy-level** problem.

It focuses on logical reasoning and arithmetic validation rather than complex algorithms, making it ideal for beginners and contest warm-ups.
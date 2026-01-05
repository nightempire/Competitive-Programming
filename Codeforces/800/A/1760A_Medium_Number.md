# A_Medium_Number

## Platform

Codeforces

## Problem Link

[A. Medium Number](https://codeforces.com/problemset/problem/1760/A)

## Problem Statement

You are given multiple test cases.
In each test case, three distinct integers are provided.

Your task is to determine and print the **medium number**, which is defined as the number that is **neither the maximum nor the minimum** among the three.

## Input Format

* The first line contains an integer `t`, representing the number of test cases.
* Each of the next `t` lines contains three integers `a`, `b`, and `c`.

## Output Format

For each test case, print a single integer — the medium number among `a`, `b`, and `c`.

Each result should be printed on a new line.

## Constraints

* `1 ≤ t ≤ 1000`
* `0 ≤ a, b, c ≤ 100`
* All three numbers in a test case are **distinct**

## Examples

### Example 1

Input

```
3
1 2 3
10 5 7
8 6 4
```

Explanation

* Test case 1: Numbers are `1, 2, 3` → medium is `2`
* Test case 2: Numbers are `10, 5, 7` → medium is `7`
* Test case 3: Numbers are `8, 6, 4` → medium is `6`

Output

```
2
7
6
```

### Example 2

Input

```
1
100 1 50
```

Explanation

* Sorted order: `1, 50, 100`
* Medium number is `50`

Output

```
50
```

## Approach (Algorithm Name / Type)

**Comparative Conditional Selection Algorithm**

This approach uses pairwise comparisons to identify the value that lies between the other two.

## Intuition

Among three distinct numbers, the medium number must satisfy one simple rule:

* It is **greater than one number and smaller than the other**

By checking this condition for each variable (`a`, `b`, and `c`), the medium value can be identified without sorting.

This avoids unnecessary overhead and keeps the solution straightforward.

## Algorithm Steps

* Read the number of test cases `t`.
* For each test case:

  * Read three integers `a`, `b`, and `c`.
  * Check whether `a` lies between `b` and `c`.
  * If not, check whether `b` lies between `a` and `c`.
  * Otherwise, `c` must be the medium number.
* Print the identified medium number.

## Visual Walkthrough

### Test Case 1

Input:

```
a = 1, b = 2, c = 3
```

Evaluation:

```
1 < 2 < 3
```

Medium number:

```
2
```

---

### Test Case 2

Input:

```
a = 10, b = 5, c = 7
```

Evaluation:

```
5 < 7 < 10
```

Medium number:

```
7
```

---

### Test Case 3

Input:

```
a = 8, b = 6, c = 4
```

Evaluation:

```
4 < 6 < 8
```

Medium number:

```
6
```

## Complexity Analysis

### Time Complexity

**O(t)**

Each test case is processed using a constant number of comparisons.
Since there are `t` test cases, the total time complexity scales linearly with `t`.

### Space Complexity

**O(1)**

Only a few integer variables are used.
No extra data structures are required.

## Solution Explanation

The solution evaluates each number to determine whether it lies between the other two using conditional checks.

Because the problem guarantees that all three numbers are distinct, exactly one number will satisfy the “middle” condition. This guarantees correctness without requiring sorting.

The logic is efficient, readable, and well-suited for competitive programming.

## Full Solution

### C++ Implementation (Heavily Commented)

```cpp
#include <iostream>
using namespace std;

int main() {

    // Number of test cases
    int t;
    cin >> t;

    // Process each test case
    while (t--) {

        // Read three distinct integers
        int a, b, c;
        cin >> a >> b >> c;

        // Check if 'a' is the medium number
        // 'a' is medium if it lies between 'b' and 'c'
        if ((a > b && a < c) || (a < b && a > c)) {
            cout << a << '\n';
        }

        // Check if 'b' is the medium number
        else if ((b > a && b < c) || (b < a && b > c)) {
            cout << b << '\n';
        }

        // If neither 'a' nor 'b' is medium, then 'c' must be the medium
        else {
            cout << c << '\n';
        }
    }

    return 0;
}
```

## Test Cases Analysis

| Input      | Explanation               | Output |
| ---------- | ------------------------- | ------ |
| `1 2 3`    | 2 lies between 1 and 3    | 2      |
| `10 5 7`   | 7 lies between 5 and 10   | 7      |
| `8 6 4`    | 6 lies between 4 and 8    | 6      |
| `100 1 50` | 50 lies between 1 and 100 | 50     |

## Edge Cases to Consider

* Minimum and maximum values at different positions
* Negative numbers (if allowed in variations)
* Single test case input

## Common Test Cases

* Already sorted numbers
* Reverse sorted numbers
* Random ordering of values

## Common Mistakes to Avoid

* Using sorting unnecessarily for just three numbers
* Incorrect logical conditions (`&&` vs `||`)
* Forgetting that all numbers are guaranteed to be distinct

## Interview Relevance

* Tests understanding of conditional logic
* Evaluates ability to reason without over-engineering
* Common screening problem for basic problem-solving skills

## What This Problem Teaches

* Efficient comparison-based logic
* Translating mathematical intuition into conditions
* Writing clean and readable decision-making code

## Key Takeaways

* Simple problems often have simple optimal solutions
* Sorting is not always required
* Clear logical conditions improve correctness and readability

## Problem Difficulty Analysis

This is an **Easy-level** problem.

It focuses on logical reasoning and conditional checks, making it ideal for beginners and quick assessments in competitive programming and interviews.
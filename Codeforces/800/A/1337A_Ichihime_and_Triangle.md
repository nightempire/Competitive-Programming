## Platform

Codeforces

## Problem Link

[A. Ichihime and Triangle](https://codeforces.com/problemset/problem/1337/A)

---

## Problem Statement

You are given four integers `a`, `b`, `c`, and `d` such that:

```text
a ≤ b ≤ c ≤ d
```

Your task is to choose three integers `x`, `y`, and `z` such that:

* `a ≤ x ≤ b`
* `b ≤ y ≤ c`
* `c ≤ z ≤ d`

and they must satisfy the **triangle inequality**:

```text
x + y > z
```

---

## Input Format

* The first line contains an integer `t` — number of test cases
* For each test case:

  * Four integers `a`, `b`, `c`, `d`

---

## Output Format

For each test case:

* Print any valid triple `x y z` satisfying the conditions

---

## Constraints

* `1 ≤ t ≤ 1000`
* `1 ≤ a ≤ b ≤ c ≤ d ≤ 10^9`

---

## Examples

### Example 1

Input

```id="r7m2xk"
3
1 2 3 4
2 3 4 5
5 5 5 5
```

Explanation

Choose:

* `x = b`
* `y = c`
* `z = c`

Check triangle:

```text
b + c > c  → always true
```

Output

```id="k8p4zn"
2 3 3
3 4 4
5 5 5
```

---

### Example 2

Input

```id="t2v9ml"
2
1 3 5 7
4 6 8 10
```

Output

```id="p6k3zs"
3 5 5
6 8 8
```

---

### Example 3

Input

```id="x4m7qp"
1
10 20 30 40
```

Output

```id="z9k2rv"
20 30 30
```

---

## Approach

Greedy constructive solution

---

## Intuition

We need to satisfy:

```text
x + y > z
```

A simple and always valid choice is:

```text
x = b  
y = c  
z = c
```

Check:

```text
b + c > c  
⇒ b > 0 (always true since b ≥ a ≥ 1)
```

Thus, this selection **always satisfies the triangle inequality**.

---

## Algorithm Steps

* Read `t`
* For each test case:

  * Read `a, b, c, d`
  * Output:

    ```
    b c c
    ```

---

## Visual Walkthrough

### Case 1: `(1, 2, 3, 4)`

```text
x = 2, y = 3, z = 3

Check:
2 + 3 > 3 → valid
```

---

### Case 2: `(2, 3, 4, 5)`

```text
x = 3, y = 4, z = 4

Check:
3 + 4 > 4 → valid
```

---

### Case 3: `(5, 5, 5, 5)`

```text
x = 5, y = 5, z = 5

Check:
5 + 5 > 5 → valid
```

---

## Complexity Analysis

### Time Complexity

O(1) per test case

* Direct output

---

### Space Complexity

O(1)

* No extra space used

---

## Solution Explanation

The solution uses a constructive approach:

* Select the largest possible values for `x` and `y`
* Keep `z` equal to `y`

This guarantees:

* Valid range constraints
* Triangle inequality satisfaction

---

## Full Solution

### C++ Implementation

```cpp
#include<iostream>
using namespace std;

int main() {

    // Number of test cases
    int t;
    cin >> t;

    while(t--) {

        // Input values
        int a, b, c, d;
        cin >> a >> b >> c >> d;

        // Construct valid triangle
        cout << b << ' ' << c << ' ' << c << '\n';
    }

    return 0;
}
```

---

## Test Cases Analysis

| a b c d | Output | Valid |
| ------- | ------ | ----- |
| 1 2 3 4 | 2 3 3  | ✔     |
| 2 3 4 5 | 3 4 4  | ✔     |
| 5 5 5 5 | 5 5 5  | ✔     |

---

## Edge Cases to Consider

* All values equal
* Minimum values
* Large values

---

## Common Test Cases

* `a = b = c = d`
* Increasing sequence
* Wide range values

---

## Common Mistakes to Avoid

* Trying complex combinations unnecessarily
* Not satisfying triangle inequality
* Picking values outside allowed ranges

---

## Interview Relevance

* Constructive algorithms
* Greedy selection
* Mathematical reasoning

---

## What This Problem Teaches

* Simple constructions can solve constraints problems
* Understanding triangle inequality
* Avoiding overcomplication

---

## Key Takeaways

* Choose boundary values smartly
* Always verify constraints
* Greedy constructions are powerful

---

## Problem Difficulty Analysis

This is an **Easy-level** problem.

It focuses on:

* Logical reasoning
* Constraint satisfaction
* Simple construction
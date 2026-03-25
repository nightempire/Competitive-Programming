## Platform

Codeforces

## Problem Link

[A. Draw a Square](https://codeforces.com/problemset/problem/2074/A)

---

## Problem Statement

You are given four integers representing the lengths of four sides.

Your task is to determine whether it is possible to form a **square** using these four sides.

A square is defined as a quadrilateral where:

* All four sides are **equal in length**

If all given sides are equal, print `"Yes"`, otherwise print `"No"`.

---

## Input Format

* The first line contains an integer `t` — the number of test cases.
* For each test case:

  * A single line contains four integers `s[0], s[1], s[2], s[3]`

---

## Output Format

For each test case:

* Print `"Yes"` if the four sides can form a square
* Otherwise, print `"No"`

---

## Constraints

* `1 ≤ t ≤ 1000`
* `1 ≤ s[i] ≤ 1000`

---

## Examples

### Example 1

Input

```
3
2 2 2 2
1 2 3 4
5 5 5 5
```

Explanation

* Case 1: All sides equal → square possible
* Case 2: Sides differ → not a square
* Case 3: All sides equal → square possible

Output

```
Yes
No
Yes
```

---

### Example 2

Input

```
2
10 10 10 10
7 7 7 8
```

Explanation

* First case → valid square
* Second case → one side differs

Output

```
Yes
No
```

---

### Example 3

Input

```
1
3 3 3 3
```

Explanation

* All sides equal → square

Output

```
Yes
```

---

## Approach

Direct comparison (uniformity check)

---

## Intuition

A square requires all four sides to be identical.

Thus, instead of complex geometry, the problem reduces to a simple condition:

```
s[0] == s[1] == s[2] == s[3]
```

If this condition holds, the shape is a square; otherwise, it is not.

---

## Algorithm Steps

* Read integer `t`
* For each test case:

  * Read four integers into an array
  * Check:

    * If all four values are equal → print `"Yes"`
    * Otherwise → print `"No"`

---

## Visual Walkthrough

### Case 1: `[2, 2, 2, 2]`

```
All sides equal → square
```

---

### Case 2: `[1, 2, 3, 4]`

```
Sides differ → not a square
```

---

### Case 3: `[5, 5, 5, 5]`

```
All sides equal → square
```

---

## Complexity Analysis

### Time Complexity

O(1) per test case

* Only constant comparisons are performed.

---

### Space Complexity

O(1)

* No extra space is used beyond a fixed-size array.

---

## Solution Explanation

The solution directly verifies whether all four side lengths are identical.

This satisfies the definition of a square. Since no ordering or geometric construction is required, a simple equality check is sufficient and optimal.

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

    // Process each test case
    while(t--) {

        // Array to store the four side lengths
        int s[4];

        // Read all four values
        cin >> s[0] >> s[1] >> s[2] >> s[3];

        // Check if all four sides are equal
        // If yes, it forms a square
        if(s[0] == s[1] && s[1] == s[2] && s[2] == s[3]) {

            // Valid square
            cout << "Yes\n";

        } else {

            // Not a square
            cout << "No\n";
        }
    }

    return 0;
}
```

---

## Test Cases Analysis

| Input   | All Equal | Output |
| ------- | --------- | ------ |
| 2 2 2 2 | Yes       | Yes    |
| 1 2 3 4 | No        | No     |
| 5 5 5 5 | Yes       | Yes    |
| 7 7 7 8 | No        | No     |

---

## Edge Cases to Consider

* Minimum values (all sides = 1)
* One side different
* All sides different
* Large equal values

---

## Common Test Cases

* `1 1 1 1` → Yes
* `2 2 2 3` → No
* `1000 1000 1000 1000` → Yes

---

## Common Mistakes to Avoid

* Comparing only pairs instead of all four values
* Missing one comparison condition
* Incorrect logical operators

---

## Interview Relevance

* Tests attention to problem constraints
* Evaluates basic condition checking
* Reinforces clarity in problem interpretation

---

## What This Problem Teaches

* Reducing problems to simple conditions
* Avoiding overcomplication
* Writing clean and direct logic

---

## Key Takeaways

* A square is fully defined by equal side lengths
* No sorting or geometry needed
* Direct comparison is optimal

---

## Problem Difficulty Analysis

This is an **Easy-level** problem.

It emphasizes:

* Basic conditional checks
* Clear understanding of definitions

Ideal for beginners and quick problem-solving practice.
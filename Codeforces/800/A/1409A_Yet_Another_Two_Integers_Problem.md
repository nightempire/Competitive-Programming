# A. Yet Another Two Integers Problem

## Platform

Codeforces

## Problem Link

[A. Yet Another Two Integers Problem](https://codeforces.com/problemset/problem/1409/A)

## Problem Statement

You are given two integers `a` and `b`.

In one move, you can increase or decrease one of the integers by **any value from 1 to 10** (inclusive).

Your task is to determine the **minimum number of moves** required to make `a` equal to `b`.

## Input Format

* The first line contains an integer `t`, the number of test cases.
* Each test case consists of a single line containing two integers:

```
a b
```

## Output Format

For each test case, print a single integer — the minimum number of moves required.

Each answer should be printed on a new line.

## Constraints

* `1 ≤ t ≤ 10^4`
* `1 ≤ a, b ≤ 10^9`

## Examples

### Example 1

Input

```
3
5 5
1 11
10 3
```

Explanation

* Test case 1: `a` is already equal to `b` → `0`
* Test case 2: difference is `10` → `1` move
* Test case 3: difference is `7` → `1` move

Output

```
0
1
1
```

### Example 2

Input

```
2
1 100
20 35
```

Explanation

* `|1 − 100| = 99` → `10` moves
* `|20 − 35| = 15` → `2` moves

Output

```
10
2
```

## Approach

**Greedy Using Maximum Allowed Step**

## Intuition

To minimize the number of moves:

* Always change the number by the **maximum allowed value (10)** whenever possible.
* Any remaining difference less than `10` can be fixed in **one final move**.

Thus, the problem reduces to dividing the absolute difference by `10` and rounding up.

## Mathematical Insight

Let:

```
diff = |a - b|
```

Then:

```
moves = ceil(diff / 10)
```

This is exactly what the code computes using integer arithmetic.

## Algorithm Steps

* Read the number of test cases
* For each test case:

  * Read integers `a` and `b`
  * Compute `diff = |a - b|`
  * Compute `diff / 10`
  * If `diff % 10 != 0`, add one extra move
  * Print the result

## Visual Walkthrough

Test case:

```
a = 20, b = 35
```

Difference:

```
diff = |20 - 35| = 15
```

Moves:

```
15 / 10 = 1
15 % 10 = 5 → remaining
Total moves = 2
```

Output:

```
2
```

Another case:

```
a = 1, b = 100
```

Difference:

```
99
```

Moves:

```
99 / 10 = 9
99 % 10 ≠ 0 → +1
Total = 10
```

## Complexity Analysis

### Time Complexity

O(t)

Each test case involves constant-time arithmetic.

### Space Complexity

O(1)

Only a few integer variables are used.

## Solution Explanation

The solution uses a greedy mathematical approach rather than simulating each move.
By taking steps of size `10` whenever possible, it guarantees the minimum number of operations.

The conditional expression handles the rounding-up behavior cleanly.

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

        // Absolute difference between a and b
        int diff = abs(a - b);

        // Number of full steps of size 10
        int count = diff / 10;

        // If there is a remainder, one more move is needed
        cout << (diff % 10 ? count + 1 : count) << '\n';
    }

    return 0;
}
```

## Test Cases Analysis

| a  | b   | diff | Moves |
| -- | --- | ---- | ----- |
| 5  | 5   | 0    | 0     |
| 1  | 11  | 10   | 1     |
| 10 | 3   | 7    | 1     |
| 20 | 35  | 15   | 2     |
| 1  | 100 | 99   | 10    |

## Edge Cases to Consider

* `a == b`
* Difference less than `10`
* Very large values of `a` and `b`

## Common Test Cases

* Difference exactly divisible by `10`
* Difference slightly above a multiple of `10`

## Common Mistakes to Avoid

* Using loops instead of arithmetic
* Forgetting absolute difference
* Off-by-one errors when handling remainders

## Interview Relevance

* Tests greedy thinking
* Reinforces integer arithmetic
* Common problem in number manipulation

## What This Problem Teaches

* Optimal use of allowed operations
* Ceiling division using integers
* Avoiding unnecessary simulation

## Key Takeaways

* Always look for mathematical simplifications
* Ceiling division is common in optimization problems
* Greedy strategies are often optimal when steps are bounded

## Problem Difficulty Analysis

This is an **Easy-level** problem.
It focuses on mathematical reasoning and efficient computation, making it suitable for beginners and competitive programming practice.
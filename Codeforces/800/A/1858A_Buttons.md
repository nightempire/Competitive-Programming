# A_Buttons

## Platform

Codeforces

## Problem Link

[A. Buttons](https://codeforces.com/problemset/problem/1858/A)

## Problem Statement

Two players, **First** and **Second**, are playing a game involving buttons.

* Player **First** has `a` buttons.
* Player **Second** has `b` buttons.
* There are `c` additional button presses that will occur.

The players take turns pressing buttons.
Your task is to determine **who will win the game** based on the values of `a`, `b`, and `c`.

The winner is decided by comparing the number of buttons after all operations, following the rules implied by the parity of `c`.

## Input Format

* The first line contains an integer `t`, the number of test cases.
* Each test case contains three integers `a`, `b`, and `c`.

## Output Format

For each test case, print:

* `First` if the first player wins
* `Second` if the second player wins

Each answer must be printed on a new line.

## Constraints

* `1 ≤ t ≤ 1000`
* `0 ≤ a, b, c ≤ 10^9`

## Examples

### Example 1

Input

```
3
1 2 1
3 1 2
5 5 3
```

Explanation

* Test case 1:

  * `c` is odd
  * Compare `a` and `b`
  * `a < b` → Second wins
* Test case 2:

  * `c` is even
  * Compare `a` and `b`
  * `a > b` → First wins
* Test case 3:

  * `c` is odd
  * `a == b` → First wins

Output

```
Second
First
First
```

## Approach

**Conditional Comparison Based on Parity**

The solution determines the winner by checking whether `c` is odd or even and then comparing `a` and `b` accordingly.

## Intuition

The key observation is that the **parity of `c`** affects whose advantage it is.

* When `c` is **odd**, the comparison favors the **First** player.
* When `c` is **even**, the comparison favors the **Second** player.

If both players have the same number of buttons, the advantage is decided purely by the parity of `c`.

## Algorithm Steps

* Read the number of test cases.
* For each test case:

  * Read values `a`, `b`, and `c`.
  * Check whether `c` is odd or even.
  * Based on parity:

    * If `c` is odd:

      * First wins when `a ≥ b`
    * If `c` is even:

      * Second wins when `a ≤ b`
* Print the winner.

## Visual Walkthrough

### Test Case 1

Input: `a = 1`, `b = 2`, `c = 1`

```
c is odd
Compare a and b
1 < 2 → Second wins
```

---

### Test Case 2

Input: `a = 3`, `b = 1`, `c = 2`

```
c is even
Compare a and b
3 > 1 → First wins
```

---

### Test Case 3

Input: `a = 5`, `b = 5`, `c = 3`

```
c is odd
a == b → First wins
```

## Complexity Analysis

### Time Complexity

O(1) per test case

Each test case involves only constant-time comparisons.

### Space Complexity

O(1)

No extra space is used beyond a few variables.

## Solution Explanation

The solution relies on a simple but crucial observation:
the outcome of the game depends entirely on whether the number of additional button presses (`c`) is odd or even.

By separating the logic based on parity and then comparing the two button counts, the winner can be determined efficiently without simulation.

## Full Solution

### C++ Implementation

```cpp
#include <iostream>
using namespace std;

int main() {

    // Number of test cases
    int t;
    cin >> t;

    while (t--) {

        int a, b, c;
        cin >> a >> b >> c;

        // If c is odd
        if (c & 1) {

            // First wins if a is greater than or equal to b
            if (a == b || a > b)
                cout << "First\n";
            else
                cout << "Second\n";

        } 
        // If c is even
        else {

            // Second wins if a is less than or equal to b
            if (a == b || a < b)
                cout << "Second\n";
            else
                cout << "First\n";
        }
    }

    return 0;
}
```

## Test Cases Analysis

| a | b | c | Parity of c | Winner |
| - | - | - | ----------- | ------ |
| 1 | 2 | 1 | Odd         | Second |
| 3 | 1 | 2 | Even        | First  |
| 5 | 5 | 3 | Odd         | First  |
| 4 | 6 | 4 | Even        | Second |

## Edge Cases to Consider

* `a == b`
* `c = 0`
* Very large values of `a`, `b`, or `c`
* Multiple test cases with mixed parity

## Common Test Cases

* Odd `c` with `a > b`
* Even `c` with `a < b`
* Equal values of `a` and `b`

## Common Mistakes to Avoid

* Ignoring the parity of `c`
* Reversing comparison conditions
* Overcomplicating with unnecessary simulation

## Interview Relevance

* Tests conditional logic clarity
* Evaluates understanding of parity-based decisions
* Common in logical reasoning and game problems

## What This Problem Teaches

* How parity can affect game outcomes
* Writing clean and minimal conditional logic
* Translating problem rules directly into comparisons

## Key Takeaways

* Always check parity when turn-based logic is involved
* Equal values often need special consideration
* Simple conditions can replace complex simulations

## Problem Difficulty Analysis

This is an **Easy-level** problem.
It focuses on logical reasoning and conditional checks rather than algorithmic complexity, making it ideal for beginners and interview warm-ups.
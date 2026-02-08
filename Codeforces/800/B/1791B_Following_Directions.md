# B_Following_Directions

## Platform

Codeforces

## Problem Link

[B. Following Directions](https://codeforces.com/problemset/problem/1791/B)

## Problem Statement

You are given a sequence of directions that a person follows on a 2D coordinate plane.

The person starts at the origin point `(0, 0)`.

Each character in the string represents a move:

* `'U'` → move up `(y + 1)`
* `'D'` → move down `(y - 1)`
* `'L'` → move left `(x - 1)`
* `'R'` → move right `(x + 1)`

Your task is to determine whether **at any point during the movement**, the person reaches the coordinate `(1, 1)`.

If the point `(1, 1)` is reached at least once, print `"YES"`.
Otherwise, print `"NO"`.

## Input Format

* The first line contains an integer `t`, the number of test cases
* For each test case:

  * An integer `n`, the length of the direction string
  * A string `s` of length `n`, consisting of characters `U`, `D`, `L`, `R`

## Output Format

* For each test case, print `"YES"` or `"NO"` on a new line

## Constraints

* `1 ≤ t ≤ 100`
* `1 ≤ n ≤ 100`
* `s[i] ∈ {'U', 'D', 'L', 'R'}`

## Examples

### Example 1

Input

```
1
4
URRD
```

Explanation

Starting at `(0, 0)`:

* `U` → `(0, 1)`
* `R` → `(1, 1)` ✅ target reached

Output

```
YES
```

---

### Example 2

Input

```
1
3
DDD
```

Explanation

All moves are downward:

* `(0, -1)`
* `(0, -2)`
* `(0, -3)`

The point `(1, 1)` is never reached.

Output

```
NO
```

---

### Example 3

Input

```
1
5
URDLU
```

Explanation

The path does not pass through `(1, 1)` at any step.

Output

```
NO
```

## Approach

**Simulation with Coordinate Tracking**

## Intuition

The path is followed step by step, and each move changes the current position.

Since we only care whether the point `(1, 1)` is **ever reached**, there is no need to store the full path:

* Track the current `(x, y)` position
* After every move, immediately check if `(x == 1 && y == 1)`

If the condition becomes true at any step, the answer is `"YES"`.

## Algorithm Steps

* Read number of test cases `t`
* For each test case:

  * Read `n` and string `s`
  * Initialize coordinates `(x, y) = (0, 0)`
  * Initialize a boolean flag as `false`
  * Traverse each character in `s`:

    * Update `(x, y)` based on the direction
    * Check if `(x == 1 && y == 1)`

      * If true, set flag and stop processing
  * Print `"YES"` if flag is true, otherwise `"NO"`

## Visual Walkthrough

### Case 1: `"UR"`

```
Start at (0, 0)
'U' → (0, 1)
'R' → (1, 1)  → target reached
```

Result: `YES`

---

### Case 2: `"RULD"`

```
(0, 0)
R → (1, 0)
U → (1, 1) → target reached
```

Result: `YES`

---

### Case 3: `"LLDD"`

```
(0, 0)
L → (-1, 0)
L → (-2, 0)
D → (-2, -1)
D → (-2, -2)
```

Target never reached.

Result: `NO`

## Complexity Analysis

### Time Complexity

**O(n)**

Each character in the direction string is processed once.

### Space Complexity

**O(1)**

Only a few integer variables are used to track coordinates.

## Solution Explanation

The solution directly simulates the movement on a 2D plane.

After each move:

* The position is updated
* A constant-time check verifies whether the target point `(1, 1)` is reached

Early termination ensures efficiency when the target is reached before processing all moves.

## Full Solution

### C++ Implementation

```cpp
#include <iostream>
using namespace std;

int main() {

    int t;
    cin >> t;

    while (t--) {

        int n;
        cin >> n;

        string s;
        cin >> s;

        // Starting coordinates
        int x = 0, y = 0;

        // Flag to track whether (1, 1) is reached
        bool flag = false;

        // Process each movement
        for (char ch : s) {

            if (ch == 'U') y++;
            else if (ch == 'R') x++;
            else if (ch == 'D') y--;
            else x--; // 'L'

            // Check if target point is reached
            if (x == 1 && y == 1) {
                flag = true;
                break;
            }
        }

        // Output result
        cout << (flag ? "YES\n" : "NO\n");
    }

    return 0;
}
```

## Test Cases Analysis

| Direction String | Path Result   | Output |
| ---------------- | ------------- | ------ |
| `UR`             | Reaches (1,1) | YES    |
| `RULD`           | Reaches (1,1) | YES    |
| `DDLL`           | Never reaches | NO     |
| `UUURRR`         | Reaches (1,1) | YES    |

## Edge Cases to Consider

* Minimum length string (`n = 1`)
* Reaching `(1, 1)` early in the path
* Paths that cross near `(1, 1)` but never land exactly on it
* Multiple test cases

## Common Test Cases

* Simple paths reaching `(1, 1)`
* Paths moving only in one direction
* Mixed-direction paths

## Common Mistakes to Avoid

* Checking only the final position instead of intermediate positions
* Incorrect coordinate updates
* Forgetting to reset coordinates for each test case

## Interview Relevance

* Tests simulation skills
* Reinforces coordinate-based movement logic
* Common path-tracking problem pattern

## What This Problem Teaches

* Step-by-step simulation
* Importance of checking intermediate states
* Clean handling of directional movement

## Key Takeaways

* Always check conditions during traversal, not just at the end
* Early termination improves efficiency
* Simple simulations can solve many geometry-based problems

## Problem Difficulty Analysis

This is an **Easy-level** problem.

It focuses on basic simulation and conditional checks, making it a frequent choice for warm-up rounds and interviews.
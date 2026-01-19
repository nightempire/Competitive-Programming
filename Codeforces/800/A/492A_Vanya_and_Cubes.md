# A_Vanya_and_Cubes

## Platform

Codeforces

## Problem Link

[A. Vanya and Cubes](https://codeforces.com/problemset/problem/492/A)

## Problem Statement

Vanya is playing with cubes. He builds a pyramid by stacking cubes level by level.

* The **first level** requires `1` cube.
* The **second level** requires `1 + 2 = 3` cubes.
* The **third level** requires `1 + 2 + 3 = 6` cubes.
* In general, the `k`-th level requires `k × (k + 1) / 2` cubes.

Given an integer `n`, representing the total number of cubes Vanya has, determine the **maximum number of complete levels** he can build.

## Input Format

* A single integer `n` — the number of cubes.

## Output Format

Print a single integer representing the maximum number of complete pyramid levels that can be built.

## Constraints

* `1 ≤ n ≤ 10^9`

## Examples

### Example 1

Input

```
1
```

Explanation

* Level 1 requires `1` cube
* Available cubes = `1`

Output

```
1
```

### Example 2

Input

```
5
```

Explanation

* Level 1 → `1` cube (remaining = 4)
* Level 2 → `3` cubes (remaining = 1)
* Level 3 → `6` cubes (not enough)

Output

```
2
```

### Example 3

Input

```
20
```

Explanation

* Level 1 → `1`
* Level 2 → `3` (total = 4)
* Level 3 → `6` (total = 10)
* Level 4 → `10` (total = 20)

Output

```
4
```

## Approach

**Greedy Iterative Accumulation Using Triangular Numbers**

The solution incrementally builds pyramid levels and keeps track of the total number of cubes used until the available cubes are exceeded.

## Intuition

Each pyramid level requires a **triangular number** of cubes.
Instead of calculating the total in advance, we can:

* Build levels one by one
* Keep adding the cubes needed for each level
* Stop when we no longer have enough cubes

This ensures that only **complete levels** are counted.

## Algorithm Steps

* Read the number of cubes `n`.
* Initialize:

  * `level = 0` (current completed levels)
  * `used = 0` (total cubes used)
* Repeat:

  * Increment `level`
  * Add cubes required for the current level
  * If `used` exceeds `n`, decrement `level` and stop
* Output the final value of `level`

## Visual Walkthrough

### Test Case 1

Input: `n = 5`

```
Level 1 → needs 1 → used = 1
Level 2 → needs 3 → used = 4
Level 3 → needs 6 → used = 10 (exceeds)
```

Maximum complete levels:

```
2
```

---

### Test Case 2

Input: `n = 20`

```
Level 1 → 1
Level 2 → 3 (total = 4)
Level 3 → 6 (total = 10)
Level 4 → 10 (total = 20)
Level 5 → 15 (exceeds)
```

Maximum complete levels:

```
4
```

## Complexity Analysis

### Time Complexity

O(√n)

The number of levels grows roughly with the square root of `n`, since the cube requirement increases quadratically.

### Space Complexity

O(1)

Only constant extra variables are used.

## Solution Explanation

The solution simulates building the pyramid level by level.
For each new level, it calculates the exact number of cubes required using the triangular number formula and adds it to the total used cubes.
As soon as the total exceeds the available cubes, the last level is discarded, ensuring the result contains only complete levels.

## Full Solution

### C++ Implementation

```cpp
#include <iostream>
using namespace std;

int main() {

    // Total number of cubes
    int n;
    cin >> n;

    // Number of complete levels built
    int level = 0;

    // Total cubes used so far
    int used = 0;

    // Build levels until cubes run out
    while (true) {

        // Move to the next level
        level++;

        // Add cubes required for the current level
        used += level * (level + 1) / 2;

        // If cubes exceed available amount, revert last level
        if (used > n) {
            level--;
            break;
        }
    }

    // Output the maximum number of complete levels
    cout << level;

    return 0;
}
```

## Test Cases Analysis

| Cubes (n) | Levels Built | Explanation                  |
| --------- | ------------ | ---------------------------- |
| 1         | 1            | Only first level possible    |
| 3         | 2            | 1 + 3 = 4 exceeds, so only 2 |
| 5         | 2            | Cannot complete third level  |
| 20        | 4            | Exactly enough cubes         |
| 100       | 6            | Seventh level exceeds        |

## Edge Cases to Consider

* Minimum value of `n`
* Exactly matching cube counts
* Large values of `n`
* Overflow prevention when summing cubes

## Common Test Cases

* Small inputs (`n < 10`)
* Inputs where cube count exactly matches a level
* Large cube counts near constraint limits

## Common Mistakes to Avoid

* Forgetting to revert the last level when exceeding cubes
* Miscalculating triangular numbers
* Using floating-point arithmetic unnecessarily

## Interview Relevance

* Demonstrates greedy problem-solving
* Uses mathematical series (triangular numbers)
* Tests loop control and boundary conditions

## What This Problem Teaches

* Applying mathematical formulas in iterative logic
* Efficient simulation techniques
* Careful handling of stopping conditions

## Key Takeaways

* Triangular numbers are useful in pyramid-style problems
* Greedy accumulation works when constraints are well-defined
* Always ensure only valid, complete structures are counted

## Problem Difficulty Analysis

This is an **Easy-level** problem.
It combines basic mathematics with simple iteration and is well-suited for beginners and interview warm-up practice.
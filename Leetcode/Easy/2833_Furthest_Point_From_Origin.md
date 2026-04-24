## 2833. Furthest Point From Origin

## Platform

LeetCode

## Problem Link

[Furthest Point From Origin](https://leetcode.com/problems/furthest-point-from-origin/)

## Problem Statement

You are given a string `moves` consisting of the characters:

* `'L'` → move left by 1 unit
* `'R'` → move right by 1 unit
* `'_'` → can be treated as either `'L'` or `'R'`

Initially, you are at position `0`.

Your task is to determine the **maximum possible distance from the origin** after performing all moves optimally.

## Input Format

* A string `moves` consisting of `'L'`, `'R'`, and `'_'`

## Output Format

* A single integer representing the maximum distance from the origin

## Constraints

* `1 ≤ moves.length ≤ 50`
* `moves[i] ∈ {'L', 'R', '_'}`

## Examples

### Example 1

Input

```id="5rjv3p"
moves = "L_RL__R"
```

Explanation

* Count L = 2, R = 2, `_` = 3
* Assign all `_` to one side (say R):

```id="t2vxsc"
Final → R = 5, L = 2 → distance = 3
```

Output

```id="6m7j4m"
3
```

---

### Example 2

Input

```id="eh9q1m"
moves = "_R__"
```

Explanation

* L = 0, R = 1, `_` = 3
* Assign all `_` to L:

```id="tov4bl"
Final → L = 3, R = 1 → distance = 2
```

Output

```id="kzj17r"
2
```

---

### Example 3

Input

```id="s7sm5v"
moves = "LRLR"
```

Explanation

* No `_` present
* L = 2, R = 2 → distance = 0

Output

```id="nt6okb"
0
```

## Approach

Greedy Counting Strategy

## Intuition

To maximize the distance from origin:

* You want to **bias all flexible moves (`_`) in one direction**
* Choose the direction that already has fewer moves, or simply maximize the imbalance

Key idea:

```text
Maximum Distance = |(L + x) - (R + y)|
Where x + y = number of '_'
```

Optimal strategy:

* Assign all `'_'` to either `'L'` or `'R'` to maximize difference

## Algorithm Steps

* Count:

  * `l` = number of `'L'`
  * `r` = number of `'R'`
  * `n` = total length
* Remaining moves (`_`) = `n - l - r`
* Assign all `_` to the side that maximizes difference:

  * If `l > r`, assign all `_` to `l`
  * Else assign all `_` to `r`
* Return `abs(l - r)`

## Visual Walkthrough

### Case 1

```id="bpxwdh"
moves = "L_R"
```

```id="dyb4n4"
L = 1, R = 1, _ = 1
Assign _ → R
Final → L=1, R=2 → distance=1
```

---

### Case 2

```id="2u0kqn"
moves = "__"
```

```id="uwwfrd"
L=0, R=0, _=2
Assign all → L or R
Distance = 2
```

---

### Case 3

```id="i3j3kq"
moves = "LLRR"
```

```id="kmx7hn"
L=2, R=2 → balanced → distance=0
```

## Complexity Analysis

### Time Complexity

**O(n)**

Single traversal to count characters.

### Space Complexity

**O(1)**

Only counters are used.

## Solution Explanation

The solution counts occurrences of `'L'` and `'R'`. The remaining positions (`'_'`) are flexible and can be assigned entirely to one direction to maximize the distance. By assigning all flexible moves to one side, we maximize the absolute difference between left and right moves.

## Full Solution

### C++ Implementation

```cpp id="c1v38j"
#include<iostream>
using namespace std;

class Solution {
public:
    int furthestDistanceFromOrigin(string moves) {

        // Total length of moves
        int n = moves.length();

        // Count of left and right moves
        int l = 0, r = 0;

        // Count occurrences
        for(char ch : moves) {
            if(ch == 'L') l++;
            else if(ch == 'R') r++;
        }

        // Remaining moves are '_'
        // Assign them optimally to maximize distance

        if(l > r)
            l = n - r;   // assign all '_' to L
        else
            r = n - l;   // assign all '_' to R

        // Return absolute distance
        return abs(l - r);
    }
};
```

## Test Cases Analysis

| moves   | L | R | _ | Optimal Assignment | Output |
| ------- | - | - | - | ------------------ | ------ |
| L_RL__R | 2 | 2 | 3 | All to one side    | 3      |
| *R*_    | 0 | 1 | 3 | All to L           | 2      |
| LRLR    | 2 | 2 | 0 | No change          | 0      |
| ____    | 0 | 0 | 4 | All one side       | 4      |

## Edge Cases to Consider

* All characters are `_`
* No `_` present
* Only one type of movement
* Minimum string length

## Common Test Cases

* Balanced `L` and `R`
* Highly skewed counts
* Only `_` characters
* Mixed scenarios

## Common Mistakes to Avoid

* Treating `_` as neutral instead of flexible
* Not assigning all `_` optimally
* Forgetting absolute value

## Interview Relevance

* Tests greedy thinking
* Evaluates ability to maximize objective function
* Common counting + optimization pattern

## What This Problem Teaches

* Converting flexibility into optimization
* Using counts instead of simulation
* Greedy assignment strategies

## Key Takeaways

* Flexible choices should be used to maximize imbalance
* Counting often replaces simulation
* Always think in terms of maximizing/minimizing expressions

## Problem Difficulty Analysis

This is an **Easy-level** problem.

The core challenge is recognizing that all flexible moves should be assigned in one direction to maximize distance, leading to a simple and efficient solution.
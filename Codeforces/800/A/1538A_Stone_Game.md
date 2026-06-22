# A. Stone Game

## Platform

Codeforces

## Problem Link

[A. Stone Game - Codeforces Problem 1538A](https://codeforces.com/problemset/problem/1538/A?utm_source=chatgpt.com)

## Problem Statement

You are given a permutation of integers from `1` to `n`, representing stones arranged in a row.

In one move, you may remove a stone from either:

* The left end of the row, or
* The right end of the row.

Your goal is to remove both:

* The smallest stone (`1`)
* The largest stone (`n`)

Determine the minimum number of moves required.

## Input Format

* The first line contains an integer `t` — the number of test cases.
* For each test case:

  * The first line contains an integer `n`.
  * The second line contains `n` distinct integers forming a permutation of `1` to `n`.

## Output Format

For each test case, print a single integer — the minimum number of moves needed to remove both stones `1` and `n`.

## Constraints

* `1 ≤ t ≤ 100`
* `2 ≤ n ≤ 100`
* The array is a permutation of integers from `1` to `n`.

## Examples

### Example 1

Input

```text
1
5
1 2 3 4 5
```

Output

```text
5
```

### Explanation

Positions:

```text
1 at index 0
5 at index 4
```

Possible strategies:

* Remove all from left → 5 moves
* Remove all from right → 5 moves
* Mixed removal → 5 moves

Minimum:

```text
5
```

---

### Example 2

Input

```text
1
5
5 2 3 4 1
```

Output

```text
2
```

### Explanation

Positions:

```text
5 at index 0
1 at index 4
```

Remove:

```text
5 from left
1 from right
```

Total moves:

```text
1 + 1 = 2
```

---

### Example 3

Input

```text
1
7
3 1 4 7 5 6 2
```

Output

```text
4
```

### Explanation

Positions:

```text
1 at index 1
7 at index 3
```

One optimal strategy:

```text
Remove first four stones from the left
```

Both target stones are removed within 4 moves.

## Approach

### Algorithm Type

Greedy Position Analysis

## Intuition

Only the positions of:

* Minimum element (`1`)
* Maximum element (`n`)

matter.

Let:

* `p1` = position of `1`
* `p2` = position of `n`

Assume:

```text
p1 ≤ p2
```

There are only three meaningful strategies:

### Strategy 1: Remove from Left Only

Remove until the farther target is reached.

Moves:

```text
p2 + 1
```

### Strategy 2: Remove from Right Only

Remove until the farther target from the right is reached.

Moves:

```text
n - p1
```

### Strategy 3: Remove from Both Ends

Remove:

* `1` from the left side
* `n` from the right side

Moves:

```text
(p1 + 1) + (n - p2)
```

The answer is the minimum among these three possibilities.

## Algorithm Steps

* Read `n`.
* Find:

  * Position of `1`
  * Position of `n`
* Ensure:

```text
p1 ≤ p2
```

by swapping if necessary.

* Compute:

  * Left-only strategy
  * Right-only strategy
  * Both-sides strategy
* Output the minimum value.

## Visual Walkthrough

### Test Case 1

Array:

```text
1 2 3 4 5
```

Positions:

```text
p1 = 0
p2 = 4
```

Strategies:

```text
Left only  = 5
Right only = 5
Both sides = 1 + 1 = 2? (Not possible simultaneously because removals affect positions)
Formula gives:
(0+1)+(5-4)=2
```

Minimum valid computation:

```text
2
```

Remove:

```text
1 from left
5 from right
```

Answer:

```text
2
```

---

### Test Case 2

Array:

```text
5 2 3 4 1
```

Positions:

```text
p1 = 4
p2 = 0
```

After ordering:

```text
p1 = 0
p2 = 4
```

Strategies:

```text
Left only  = 5
Right only = 5
Both sides = 2
```

Answer:

```text
2
```

---

### Test Case 3

Array:

```text
3 1 4 7 5 6 2
```

Positions:

```text
p1 = 1
p2 = 3
```

Strategies:

```text
Left only  = 4
Right only = 6
Both sides = 2 + 4 = 6
```

Answer:

```text
4
```

## Complexity Analysis

### Time Complexity

**O(n)**

The array is scanned once to locate:

* `1`
* `n`

All remaining operations are constant time.

```text
O(n)
```

### Space Complexity

**O(1)**

Only a few integer variables are used.

```text
O(1)
```

## Solution Explanation

The solution first finds the positions of the smallest and largest stones.

Since only these two stones need to be removed, all other values are irrelevant.

After locating their positions, the algorithm evaluates the three possible optimal strategies:

1. Remove everything from the left.
2. Remove everything from the right.
3. Remove some stones from both ends.

The minimum among these values is the answer.

This greedy observation eliminates the need for simulation.

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

        // Size of permutation
        int n;
        cin >> n;

        // Positions of 1 and n
        int p1, p2;

        // Read permutation and locate targets
        for(int i = 0; i < n; i++) {

            int num;
            cin >> num;

            if(num == 1) {
                p1 = i;
            }
            else if(num == n) {
                p2 = i;
            }
        }

        // Ensure p1 <= p2
        if(p1 > p2) {

            int temp = p1;
            p1 = p2;
            p2 = temp;
        }

        // Compute minimum among:
        // 1. Remove from right only
        // 2. Remove from left only
        // 3. Remove from both sides
        cout << min(
                    n - p1,
                    min(
                        p2 + 1,
                        p1 + 1 + n - p2
                    )
                ) << '\n';
    }

    return 0;
}
```

## Test Cases Analysis

| Permutation   | Position of 1 | Position of n | Minimum Moves |
| ------------- | ------------- | ------------- | ------------- |
| 1 2 3 4 5     | 0             | 4             | 2             |
| 5 2 3 4 1     | 4             | 0             | 2             |
| 3 1 4 7 5 6 2 | 1             | 3             | 4             |
| 2 1           | 1             | 0             | 2             |
| 1 3 2         | 0             | 1             | 2             |

## Edge Cases to Consider

* `1` and `n` are at opposite ends.
* `1` and `n` are adjacent.
* `1` is at the beginning.
* `n` is at the end.
* Minimum array size (`n = 2`).
* Both targets located near the same side.

## Common Test Cases

### Targets at Opposite Ends

```text
Input:
1
5
1 2 3 4 5

Output:
2
```

---

### Targets Near Left Side

```text
Input:
1
5
1 5 2 3 4

Output:
2
```

---

### Targets Near Right Side

```text
Input:
1
5
2 3 4 1 5

Output:
2
```

---

### Mixed Position

```text
Input:
1
7
3 1 4 7 5 6 2

Output:
4
```

## Common Mistakes to Avoid

* Forgetting to reorder positions so that `p1 ≤ p2`.
* Considering only left-only and right-only removals while ignoring the mixed strategy.
* Simulating removals unnecessarily instead of analyzing positions directly.

## Interview Relevance

* Demonstrates greedy optimization through observation.
* Tests array indexing and position tracking.
* Shows how to reduce a problem to a few candidate strategies.

## What This Problem Teaches

* Position-based reasoning.
* Greedy minimization techniques.
* Evaluating all optimal boundary-removal strategies.

## Key Takeaways

* Only the positions of `1` and `n` matter.
* Many array-removal problems can be solved without simulation.
* Considering all boundary-removal combinations often leads to an optimal solution.

## Problem Difficulty Analysis

This is an **Easy** greedy problem.

The challenge is recognizing that only three candidate strategies need to be evaluated. Once the positions of the minimum and maximum elements are known, the answer can be computed directly in constant time after a single array scan.
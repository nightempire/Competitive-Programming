# A. New Year and Hurry

## Platform

Codeforces

## Problem Link

[A. New Year and Hurry](https://codeforces.com/problemset/problem/750/A)

## Problem Statement

A contestant plans to solve problems before a New Year party.

* There are `n` problems in total.
* Solving the `i`-th problem takes `5 × i` minutes.
* The contest lasts `240` minutes.
* The contestant spends `k` minutes commuting to the party.

Determine the **maximum number of problems** the contestant can solve before leaving.

## Input Format

A single line containing two integers:

```
n k
```

## Output Format

Print a single integer representing the maximum number of problems that can be solved.

## Constraints

* `1 ≤ n ≤ 10`
* `0 ≤ k ≤ 240`

## Examples

### Example 1

Input

```
3 222
```

Explanation

Available time:

```
240 − 222 = 18 minutes
```

Problem times:

```
Problem 1 → 5 minutes
Problem 2 → 10 minutes
Problem 3 → 15 minutes
```

Only the first two problems fit.

Output

```
2
```

### Example 2

Input

```
10 0
```

Explanation
All 240 minutes are available. The contestant can solve as many problems as time allows.

Output

```
9
```

### Example 3

Input

```
1 240
```

Explanation
No time remains after commuting.

Output

```
0
```

## Approach

**Greedy Accumulation Based on Increasing Cost**

## Intuition

Each subsequent problem takes more time than the previous one.
To maximize the number of solved problems, the contestant should solve problems in order, stopping as soon as the remaining time is insufficient.

## Algorithm Steps

* Read the number of problems and commute time
* Compute the remaining available time
* Iterate from problem `1` to `n`
* For each problem:

  * Check if the remaining time is sufficient
  * Deduct the required time
* Stop when time is insufficient
* Output the count of solved problems

## Visual Walkthrough

Input:

```
n = 3, k = 222
```

Remaining time:

```
240 − 222 = 18
```

Step-by-step:

```
Problem 1 → needs 5  → remaining 13
Problem 2 → needs 10 → remaining 3
Problem 3 → needs 15 → not enough time
```

Solved problems:

```
2
```

Another case:

```
n = 1, k = 240
Remaining time = 0
```

No problems can be solved.

## Complexity Analysis

### Time Complexity

O(n)

Each problem is checked once.

### Space Complexity

O(1)

Only constant extra variables are used.

## Solution Explanation

The solution subtracts the commute time from the total contest duration and then greedily solves problems in increasing order of time requirement. Since problem times grow linearly, this approach guarantees the maximum number of solved problems.

## Full Solution

### C++ Implementation

```cpp
#include <iostream>
using namespace std;

int main() {

    // n -> total number of problems
    // k -> minutes spent commuting
    int n, k, i;
    cin >> n >> k;

    // Total contest time is 240 minutes
    // Subtract commuting time to get available time
    int time = 240 - k;

    // Try solving problems one by one
    for (i = 1; i <= n; i++) {

        // Time required for problem i is 5 * i minutes
        if (time < 5 * i) {
            break;  // Not enough time to solve this problem
        }

        // Deduct time for the solved problem
        time -= 5 * i;
    }

    // i - 1 gives the number of problems successfully solved
    cout << i - 1 << '\n';

    return 0;
}
```

## Test Cases Analysis

| n  | k   | Solved Problems |
| -- | --- | --------------- |
| 3  | 222 | 2               |
| 10 | 0   | 9               |
| 1  | 240 | 0               |
| 5  | 200 | 1               |

## Edge Cases to Consider

* No time available after commuting
* Only one problem
* Enough time for all problems

## Common Test Cases

* Maximum commute time
* Zero commute time
* Partial completion scenarios

## Common Mistakes to Avoid

* Forgetting to subtract commute time
* Miscalculating time per problem
* Off-by-one errors in loop handling

## Interview Relevance

* Demonstrates greedy strategy
* Tests loop control and condition checks
* Evaluates time-management logic

## What This Problem Teaches

* Efficient resource utilization
* Importance of early termination conditions
* Translating real-world constraints into code

## Key Takeaways

* Greedy approaches are effective when costs increase monotonically
* Always account for fixed overhead before processing
* Clear loop boundaries prevent logical errors

## Problem Difficulty Analysis

This is an **Easy-level** problem.
It focuses on simple arithmetic and greedy iteration, making it ideal for beginners and interview warm-up sessions.
## 1999C. Showering

## Platform

Codeforces

## Problem Link

[Showering](https://codeforces.com/problemset/problem/1999/C)

## Problem Statement

Monocarp has a schedule consisting of several occupied time intervals during a day.

The day starts at time `0` and ends at time `m`.

Monocarp wants to take a shower that requires exactly `s` units of uninterrupted time.

You are given `n` occupied intervals. Determine whether there exists at least one free time segment of length at least `s` where Monocarp can take a shower.

## Input Format

* The first line contains an integer `t`, the number of test cases.
* For each test case:

  * The first line contains three integers `n`, `s`, and `m`.

    * `n` = number of occupied intervals
    * `s` = required shower duration
    * `m` = end time of the day
  * The next `n` lines contain two integers `l` and `r`, representing an occupied interval `[l, r]`.

## Output Format

* For each test case, print:

  * `"YES"` if there exists a free interval of length at least `s`
  * `"NO"` otherwise

## Constraints

* `1 ≤ t ≤ 10^4`
* `1 ≤ n ≤ 2 × 10^5`
* `1 ≤ s ≤ m ≤ 10^9`
* `0 ≤ l < r ≤ m`
* Intervals are given in increasing order and do not overlap
* Sum of all `n` across test cases does not exceed `2 × 10^5`

## Examples

### Example 1

Input

```text
1
3 2 10
1 3
5 6
8 9
```

Explanation

Free intervals:

```text
[0,1] → length 1
[3,5] → length 2
[6,8] → length 2
[9,10] → length 1
```

A free interval of length `2` exists.

Output

```text
YES
```

---

### Example 2

Input

```text
1
2 4 10
2 5
6 9
```

Explanation

Free intervals:

```text
[0,2] → length 2
[5,6] → length 1
[9,10] → length 1
```

No free interval has length at least `4`.

Output

```text
NO
```

---

### Example 3

Input

```text
1
1 3 10
4 6
```

Explanation

Free intervals:

```text
[0,4] → length 4
[6,10] → length 4
```

Either interval can accommodate the shower.

Output

```text
YES
```

## Approach

Interval Gap Analysis (Greedy Traversal)

## Intuition

The occupied intervals divide the day into free segments.

To determine whether a shower is possible:

* Check the gap before the first interval.
* Check gaps between consecutive intervals.
* Check the gap after the last interval.

If any free segment has length at least `s`, the answer is `"YES"`.

## Algorithm Steps

* Read number of test cases `t`.
* For each test case:

  * Read `n`, `s`, and `m`.
  * Initialize `start = 0`.
  * For every occupied interval:

    * Compute the free gap:

      ```text
      interval_start - start
      ```

    * If the gap is at least `s`, mark answer as possible.

    * Update:

      ```text
      start = interval_end
      ```
  * After processing all intervals, check:

    ```text
    m - start
    ```

    which represents the final free segment.
  * If any valid gap exists, print `"YES"`, otherwise print `"NO"`.

## Visual Walkthrough

### Case 1

```text
n = 3, s = 2, m = 10

Intervals:
[1,3]
[5,6]
[8,9]
```

Timeline:

```text
0---1 XXX 3---5 X 6---8 X 9---10
```

Gap lengths:

```text
1, 2, 2, 1
```

A gap of length `2` exists.

Answer:

```text
YES
```

---

### Case 2

```text
n = 2, s = 4, m = 10

Intervals:
[2,5]
[6,9]
```

Timeline:

```text
0--2 XXX 5-6 XXX 9-10
```

Gap lengths:

```text
2, 1, 1
```

No gap is at least `4`.

Answer:

```text
NO
```

---

### Case 3

```text
n = 1, s = 3, m = 10

Interval:
[4,6]
```

Timeline:

```text
0----4 XXX 6----10
```

Gap lengths:

```text
4, 4
```

A valid free segment exists.

Answer:

```text
YES
```

## Complexity Analysis

### Time Complexity

**O(n)** per test case

Each interval is processed exactly once.

### Space Complexity

**O(n)**

The given solution stores all intervals in an array before processing them.

## Solution Explanation

The solution keeps track of the end of the previously occupied interval using the variable `start`.

For every interval:

* The difference between the current interval's start time and `start` gives the available free time.
* If that free time is at least `s`, a shower can be scheduled.

After processing all intervals, the remaining time from the end of the last interval to `m` is checked as well.

If any free segment satisfies the required duration, the answer is `"YES"`.

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

        // Number of intervals,
        // required shower duration,
        // end of the day
        int n, s, m;

        cin >> n >> s >> m;

        // Stores end of previous occupied interval
        int start = 0;

        // Store intervals
        int intervals[n][2];

        // Flag indicating whether a valid gap exists
        bool flag = false;

        for(int i = 0; i < n; i++) {

            cin >> intervals[i][0] >> intervals[i][1];

            // Check free time before current interval
            if(s <= intervals[i][0] - start) {
                flag = true;
            }

            // Update previous ending point
            start = intervals[i][1];
        }

        // Check free time after the last interval
        if(s <= m - start) {
            flag = true;
        }

        // Output result
        cout << (flag ? "YES\n" : "NO\n");
    }

    return 0;
}
```

## Test Cases Analysis

| n | s | m  | Intervals           | Largest Free Gap | Output |
| - | - | -- | ------------------- | ---------------- | ------ |
| 3 | 2 | 10 | [1,3], [5,6], [8,9] | 2                | YES    |
| 2 | 4 | 10 | [2,5], [6,9]        | 2                | NO     |
| 1 | 3 | 10 | [4,6]               | 4                | YES    |
| 1 | 5 | 10 | [0,10]              | 0                | NO     |

## Edge Cases to Consider

* Free time exists before the first interval
* Free time exists after the last interval
* Only one interval occupies the whole day
* Required shower duration equals a gap exactly
* No occupied intervals (if allowed by constraints)

## Common Test Cases

* Gap at the beginning of the day
* Gap in the middle of the day
* Gap at the end of the day
* Multiple small gaps but none large enough
* Gap length exactly equal to `s`

## Common Mistakes to Avoid

* Forgetting to check the gap before the first interval
* Forgetting to check the gap after the last interval
* Using `>` instead of `>=` when comparing gap length with `s`

## Interview Relevance

* Tests interval processing fundamentals
* Demonstrates gap detection in schedules
* Common pattern in calendar and scheduling problems

## What This Problem Teaches

* Working with intervals efficiently
* Detecting free segments between occupied ranges
* Using greedy traversal for schedule analysis

## Key Takeaways

* Interval-gap problems are often solved with a single linear scan.
* Always check boundary gaps (start and end).
* Comparing consecutive intervals is sufficient to find all free segments.

## Problem Difficulty Analysis

This is an **Easy-level** problem.

The solution requires only a straightforward traversal of the intervals while checking the lengths of free gaps. The primary challenge is ensuring that the gaps at the beginning and end of the timeline are also considered.
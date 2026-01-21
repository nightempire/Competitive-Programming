# A_Minutes_Before_the_New_Year

## Platform

Codeforces

## Problem Link

[A. Minutes Before the New Year](https://codeforces.com/problemset/problem/1283/A)

## Problem Statement

New Year is approaching, and the clock shows the current time in hours and minutes.

Given the current time in **24-hour format**, determine how many **minutes remain until midnight (00:00)** of the next day.

This calculation must be done independently for multiple test cases.

## Input Format

* The first line contains an integer `t`, the number of test cases.
* Each test case consists of:

  * An integer `h` — current hour
  * An integer `m` — current minute

## Output Format

For each test case, print a single integer representing the number of minutes remaining until the New Year.

Each answer should be printed on a new line.

## Constraints

* `1 ≤ t ≤ 1440`
* `0 ≤ h ≤ 23`
* `0 ≤ m ≤ 59`

## Examples

### Example 1

Input

```
3
23 0
23 59
0 1
```

Explanation

* Case 1: From 23:00 to 24:00 → 60 minutes
* Case 2: From 23:59 to 24:00 → 1 minute
* Case 3: From 00:01 to 24:00 → 1439 minutes

Output

```
60
1
1439
```

### Example 2

Input

```
2
12 30
0 0
```

Explanation

* Case 1: From 12:30 to midnight → 690 minutes
* Case 2: Already at midnight → 1440 minutes remain in the day

Output

```
690
1440
```

## Approach

**Time Conversion and Arithmetic Calculation**

## Intuition

A full day contains **1440 minutes**.

The idea is to:

* Convert the current time into minutes passed since `00:00`
* Subtract this value from the total number of minutes in a day

This directly yields the number of minutes remaining until midnight.

## Algorithm Steps

* Read the number of test cases `t`
* For each test case:

  * Read `h` and `m`
  * Compute remaining minutes using:

    ```
    remaining = (24 - h) * 60 - m
    ```
  * Print the result

## Visual Walkthrough

### Test Case 1

Input time:

```
23:00
```

Calculation:

```
(24 - 23) × 60 − 0 = 60
```

Remaining minutes:

```
60
```

---

### Test Case 2

Input time:

```
23:59
```

Calculation:

```
(24 - 23) × 60 − 59 = 1
```

Remaining minutes:

```
1
```

---

### Test Case 3

Input time:

```
00:01
```

Calculation:

```
(24 - 0) × 60 − 1 = 1439
```

Remaining minutes:

```
1439
```

## Complexity Analysis

### Time Complexity

**O(t)**

Each test case involves constant-time arithmetic operations.

### Space Complexity

**O(1)**

Only fixed-size variables are used for computation.

## Solution Explanation

The solution avoids unnecessary conversions or loops by directly applying arithmetic on hours and minutes. By determining how many minutes are left in the current hour block and the remaining hours of the day, the result is obtained in a single expression. This makes the solution both efficient and easy to understand.

## Full Solution

### C++ Implementation

```cpp
#include <iostream>
using namespace std;

int main() {

    // Number of test cases
    int t;
    cin >> t;

    // Process each test case independently
    while (t--) {

        // Current hour and minute
        int h, m;
        cin >> h >> m;

        // Calculate minutes remaining until midnight
        // (24 - h) gives remaining hours
        // Multiply by 60 to convert hours to minutes
        // Subtract current minutes 'm'
        int remainingMinutes = (24 - h) * 60 - m;

        // Output the result
        cout << remainingMinutes << '\n';
    }

    return 0;
}
```

## Test Cases Analysis

| Input Time | Expected Output | Reasoning                       |
| ---------- | --------------- | ------------------------------- |
| `23 00`    | `60`            | One hour left                   |
| `23 59`    | `1`             | One minute left                 |
| `0 0`      | `1440`          | Full day remaining              |
| `12 30`    | `690`           | Half day plus 30 minutes passed |

## Edge Cases to Consider

* Time exactly at midnight (`00:00`)
* Time just before midnight (`23:59`)
* Early morning times
* Maximum number of test cases

## Common Test Cases

* Boundary values of hours and minutes
* Random mid-day times
* Sequential times approaching midnight

## Common Mistakes to Avoid

* Forgetting to subtract current minutes
* Using `23 - h` instead of `24 - h`
* Incorrect handling of `00:00`

## Interview Relevance

* Tests understanding of time calculations
* Evaluates arithmetic simplification
* Common warm-up problem in interviews

## What This Problem Teaches

* Converting real-world time problems into math
* Using simple formulas instead of simulation
* Handling edge cases cleanly

## Key Takeaways

* Time-based problems often reduce to unit conversion
* Direct arithmetic leads to cleaner solutions
* Clear constraints simplify implementation

## Problem Difficulty Analysis

This is an **Easy-level** problem.
It focuses on basic arithmetic and logical thinking, making it ideal for beginners and quick interview warm-up practice.
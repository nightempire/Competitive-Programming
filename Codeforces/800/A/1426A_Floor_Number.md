# A. Floor Number

## Platform

Codeforces

## Problem Link

[A. Floor Number](https://codeforces.com/problemset/problem/1426/A)

## Problem Statement

You are given two integers `n` and `x`.

A building has the following structure:

* The **first floor** contains **2 apartments**
* Every floor above the first contains **`x` apartments**

Apartment numbering starts from `1` and increases sequentially.

Your task is to determine **on which floor apartment number `n` is located**.

## Input Format

* The first line contains an integer `t`, the number of test cases.
* For each test case:

  * A line containing two integers `n` and `x`.

## Output Format

For each test case, print a single integer — the floor number where apartment `n` is located.

## Constraints

* `1 ≤ t ≤ 10⁴`
* `1 ≤ n, x ≤ 10⁹`

## Examples

### Example 1

Input

```
3
1 3
2 3
3 3
```

Explanation

* Apartment `1` → Floor `1`
* Apartment `2` → Floor `1`
* Apartment `3` → Floor `2`

Output

```
1
1
2
```

---

### Example 2

Input

```
1
10 3
```

Explanation

* First floor covers apartments `1` and `2`
* Remaining apartments: `3` to `10` → `8` apartments
* Each floor has `3` apartments

Floors needed above first:

```
ceil(8 / 3) = 3
```

Total floor:

```
1 + 3 = 4
```

Output

```
4
```

## Approach

**Mathematical computation using ceiling division**

## Intuition

The first floor is special because it contains exactly **2 apartments**.

All remaining apartments follow a regular pattern:

* Each floor contains `x` apartments
* Apartment `n` beyond the first two can be mapped using division

By reducing the problem to counting how many full `x`-sized groups fit after apartment `2`, the floor number can be computed directly.

## Algorithm Steps

* Read the number of test cases.
* For each test case:

  * Subtract `2` from `n` to exclude the first floor apartments.
  * If the remaining value is less than `1`, the apartment is on floor `1`.
  * Otherwise:

    * Compute how many full groups of size `x` are needed.
    * Add `1` to account for the first floor.
* Print the computed floor number.

## Visual Walkthrough

### Case 1

```
n = 1
```

Apartment lies in:

```
[1, 2] → Floor 1
```

---

### Case 2

```
n = 7, x = 3
```

Remaining apartments after first floor:

```
7 − 2 = 5
```

Grouping:

```
ceil(5 / 3) = 2 floors
```

Total:

```
1 + 2 = 3
```

---

### Case 3

```
n = 2
```

Still on:

```
Floor 1
```

## Complexity Analysis

### Time Complexity

**O(1) per test case**

Only arithmetic operations are used.

### Space Complexity

**O(1)**

No additional data structures are required.

## Solution Explanation

The solution treats the first floor separately due to its unique size.

By subtracting the first two apartments and applying ceiling division on the remaining apartments, the floor number is determined efficiently without loops or simulations.

This guarantees correctness even for very large values of `n`.

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

        // n -> apartment number
        // x -> apartments per floor (after first floor)
        int n, x;
        cin >> n >> x;

        int floor = 0;

        // Remove apartments on the first floor
        n -= 2;

        // If apartment lies on the first floor
        if (n < 1) {
            floor = 1;
        }
        // Otherwise compute floor using ceiling division
        else {
            floor = n / x + (n % x ? 1 : 0) + 1;
        }

        // Output the floor number
        cout << floor << '\n';
    }

    return 0;
}
```

## Test Cases Analysis

| n  | x | Remaining | Floor |
| -- | - | --------- | ----- |
| 1  | 3 | —         | 1     |
| 2  | 3 | —         | 1     |
| 3  | 3 | 1         | 2     |
| 7  | 3 | 5         | 3     |
| 10 | 3 | 8         | 4     |

## Edge Cases to Consider

* `n = 1` or `n = 2`
* Very large `n`
* `x = 1`
* Minimal valid inputs

## Common Test Cases

* Apartments on the first floor
* Apartments exactly at floor boundaries
* Large values requiring multiple floors

## Common Mistakes to Avoid

* Forgetting that the first floor has only 2 apartments
* Incorrect ceiling division
* Off-by-one errors when adding the first floor

## Interview Relevance

* Tests mathematical reasoning
* Evaluates careful handling of special cases
* Common arithmetic-based logic problem

## What This Problem Teaches

* Handling special base cases
* Using ceiling division correctly
* Translating real-world rules into formulas

## Key Takeaways

* Separate irregular cases before generalizing
* Arithmetic solutions outperform simulation
* Clear problem modeling simplifies implementation

## Problem Difficulty Analysis

This is an **Easy-level** problem.

It focuses on mathematical reasoning and edge-case handling, making it suitable for beginners and competitive programming warm-ups.
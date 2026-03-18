# A_Cards_for_Friends

## Platform

Codeforces

## Problem Link

[A. Cards for Friends](https://codeforces.com/problemset/problem/1472/A)

## Problem Statement

You are given a rectangular sheet of size `w × h`.

You can perform the following operation:

* If one side of the sheet is **even**, you can cut it into two equal halves along that side.

Each cut doubles the number of sheets.

Your goal is to determine whether it is possible to obtain **at least `n` sheets** by performing such cuts.

## Input Format

* The first line contains an integer `t` — the number of test cases.
* Each test case contains three integers:

```text
w h n
```

## Output Format

For each test case, print:

```
YES
```

if it is possible to obtain at least `n` sheets, otherwise:

```
NO
```

## Constraints

* `1 ≤ t ≤ 1000`
* `1 ≤ w, h ≤ 10^9`
* `1 ≤ n ≤ 10^9`

## Examples

### Example 1

Input

```
3
2 2 3
3 3 2
4 2 4
```

Explanation

Test Case 1

```
w = 2, h = 2
```

Cuts:

```
2 → 1 (cut)
2 → 1 (cut)
```

Total sheets:

```
2 × 2 = 4
```

Since `4 ≥ 3`, answer is:

```
YES
```

---

Test Case 2

```
w = 3, h = 3
```

No cuts possible (both odd).

Sheets:

```
1
```

Since `1 < 2`, answer is:

```
NO
```

---

Test Case 3

```
w = 4, h = 2
```

Cuts:

```
4 → 2 → 1  (2 cuts → 4 pieces)
2 → 1      (1 cut → 2 pieces)
```

Total sheets:

```
4 × 2 = 8
```

Since `8 ≥ 4`, answer is:

```
YES
```

## Approach

Greedy Factorization using Powers of 2

## Intuition

Each time we divide a side by `2`, we double the number of sheets.

So the total number of sheets depends on how many times `w` and `h` can be divided by `2`.

Let:

```
w = 2^a × x
h = 2^b × y
```

Where `x` and `y` are odd.

Then:

```
total sheets = 2^(a + b)
```

So we only need to count how many times `w` and `h` are divisible by `2`.

## Algorithm Steps

* Read integer `t`.
* For each test case:

  * Read `w`, `h`, `n`.
  * Count how many times `w` is divisible by `2`.
  * Count how many times `h` is divisible by `2`.
  * Total sheets:

```
sheets = 2^(count_w + count_h)
```

* If `sheets ≥ n`:

  * Print `"YES"`
* Else:

  * Print `"NO"`

## Visual Walkthrough

### Test Case 1

Input

```
w = 2, h = 2
```

Factorization:

```
2 = 2^1
2 = 2^1
```

Total:

```
2^(1+1) = 4
```

Check:

```
4 ≥ 3 → YES
```

---

### Test Case 2

Input

```
w = 3, h = 3
```

Factorization:

```
3 = 2^0
3 = 2^0
```

Total:

```
2^0 = 1
```

Check:

```
1 < 2 → NO
```

---

### Test Case 3

Input

```
w = 4, h = 2
```

Factorization:

```
4 = 2^2
2 = 2^1
```

Total:

```
2^(2+1) = 8
```

Check:

```
8 ≥ 4 → YES
```

## Complexity Analysis

### Time Complexity

```
O(log w + log h)
```

Each division by 2 reduces the number quickly.

### Space Complexity

```
O(1)
```

Only a few variables are used.

## Solution Explanation

The function:

```cpp
int cuts(int& x)
```

counts how many times a number can be divided by 2.

For each such division, the number of sheets doubles.

Thus:

```
total sheets = 2^(cuts(w) + cuts(h))
```

The program checks whether this number is sufficient to meet the requirement `n`.

## Full Solution

### C++ Implementation

```cpp
#include<iostream>
using namespace std;

// Function to count how many times x is divisible by 2
int cuts(int& x) {

    int count = 0;

    // Keep dividing while x is even
    while ((x & 1) == 0) {

        x /= 2;
        count++;
    }

    return count;
}

int main() {

    int t, w, h, n;
    cin >> t;

    while (t--) {

        cin >> w >> h >> n;

        // Count factors of 2 in w and h
        int total_cuts = cuts(w) + cuts(h);

        // Total sheets = 2^(total_cuts)
        int sheets = 1 << total_cuts;

        // Check if enough sheets can be formed
        if (sheets >= n)
            cout << "YES\n";
        else
            cout << "NO\n";
    }

    return 0;
}
```

## Test Cases Analysis

| w | h | Factors of 2 | Sheets | n | Result |
| - | - | ------------ | ------ | - | ------ |
| 2 | 2 | 1+1          | 4      | 3 | YES    |
| 3 | 3 | 0+0          | 1      | 2 | NO     |
| 4 | 2 | 2+1          | 8      | 4 | YES    |
| 8 | 1 | 3+0          | 8      | 5 | YES    |

## Edge Cases to Consider

* Both `w` and `h` are odd
* `n = 1`
* Very large `w`, `h`
* Only one dimension divisible by 2

## Common Test Cases

```
2 2 3
3 3 2
4 2 4
8 1 8
1 1 1
```

## Common Mistakes to Avoid

* Forgetting to multiply contributions from both dimensions
* Using multiplication instead of exponentiation logic
* Not handling large values correctly

## Interview Relevance

* Demonstrates factorization techniques
* Shows understanding of bit manipulation
* Introduces exponential growth reasoning

## What This Problem Teaches

* Breaking problems into prime factors
* Efficient counting using division
* Using bitwise operations for optimization

## Key Takeaways

* Repeated division by 2 corresponds to powers of 2
* Each cut doubles the number of sheets
* Total sheets depend on combined factors of both dimensions

## Problem Difficulty Analysis

This is an **Easy-level** problem.

It mainly requires understanding how repeated division affects growth and translating that into a power-of-two calculation.
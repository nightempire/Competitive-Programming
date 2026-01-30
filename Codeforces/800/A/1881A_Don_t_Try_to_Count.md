# A. Don't Try to Count

## Platform

Codeforces

## Problem Link

[A. Don't Try to Count](https://codeforces.com/problemset/problem/1881/A)

## Problem Statement

You are given two strings:

* `x` — an initial string
* `s` — a target string

You are allowed to perform the following operation **at most 10 times**:

* Replace `x` with `x + x` (concatenate the string with itself)

Your task is to determine the **minimum number of operations** required such that `s` becomes a **substring of `x`**.

If it is impossible to make `s` a substring of `x` within 10 operations, output `-1`.

## Input Format

* The first line contains an integer `t`, the number of test cases.
* For each test case:

  * Two integers `n` and `m` — lengths of strings `x` and `s`.
  * A string `x`.
  * A string `s`.

## Output Format

For each test case, print a single integer:

* The minimum number of operations needed to make `s` a substring of `x`
* `-1` if it is not possible within 10 operations

## Constraints

* `1 ≤ t ≤ 10⁴`
* `1 ≤ n, m ≤ 100`
* Strings consist of lowercase English letters

## Examples

### Example 1

Input

```
1
1 2
a
aa
```

Explanation

Initial `x = "a"`

Operations:

```
1st → "aa"
```

Substring found after `1` operation.

Output

```
1
```

---

### Example 2

Input

```
1
2 3
ab
bab
```

Explanation

Operations:

```
ab → abab → ababab
```

Substring `"bab"` appears after `2` operations.

Output

```
2
```

---

### Example 3

Input

```
1
1 3
a
bbb
```

Explanation

Even after 10 doublings, `"bbb"` never appears.

Output

```
-1
```

## Approach

**Greedy string doubling with substring search**

## Intuition

Each operation **doubles the size of `x`**, rapidly increasing its length.

Since the length grows exponentially, checking up to **10 doublings** is sufficient to cover all feasible cases under constraints.

At every step, we simply check whether `s` exists as a substring of the current `x`.

## Algorithm Steps

* Read the number of test cases.
* For each test case:

  * Read `n`, `m`, `x`, and `s`.
  * Initialize `count = 0`.
  * Repeat up to 10 times:

    * If `s` is a substring of `x`, store `count` as the answer and stop.
    * Otherwise, update `x = x + x` and increment `count`.
  * If `s` is never found, output `-1`.

## Visual Walkthrough

### Case 1

```
x = "a", s = "aa"
```

```
Step 0: "a"      → not found
Step 1: "aa"     → found
```

Answer = `1`

---

### Case 2

```
x = "ab", s = "bab"
```

```
Step 0: "ab"
Step 1: "abab"
Step 2: "ababab" → found
```

Answer = `2`

---

### Case 3

```
x = "a", s = "bbb"
```

No substring found after 10 steps → `-1`

## Complexity Analysis

### Time Complexity

**O(10 × |x| × |s|)**

At most 10 substring searches are performed.

### Space Complexity

**O(|x|)**

The string grows due to concatenation.

## Solution Explanation

The solution repeatedly doubles the string `x` and checks whether `s` appears as a substring.

Because the string length grows exponentially, the search space becomes large very quickly, and checking beyond 10 iterations is unnecessary.

This greedy approach ensures correctness while remaining efficient.

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

        // Lengths of strings x and s
        int n, m;
        cin >> n >> m;

        // Strings x and s
        string x, s;
        cin >> x >> s;

        // Answer and operation counter
        int ans = -1;
        int count = 0;

        // Try at most 10 doublings
        for (int i = 0; i <= 10; i++) {

            // Check if s is a substring of x
            if (x.find(s) != -1) {
                ans = count;
                break;
            }

            // Double the string x
            x += x;
            count++;
        }

        // Output the result
        cout << ans << '\n';
    }

    return 0;
}
```

## Test Cases Analysis

| x   | s   | Operations | Output |
| --- | --- | ---------- | ------ |
| a   | aa  | 1          | 1      |
| ab  | bab | 2          | 2      |
| a   | bbb | >10        | -1     |
| abc | abc | 0          | 0      |

## Edge Cases to Consider

* `s` already a substring of `x`
* `s` longer than any possible doubled `x`
* Maximum allowed doublings reached
* Single-character strings

## Common Test Cases

* Repeated characters
* Overlapping substrings
* Impossible substring cases

## Common Mistakes to Avoid

* Forgetting to limit operations to 10
* Doubling before checking the initial string
* Incorrect substring search condition

## Interview Relevance

* Tests string manipulation
* Demonstrates greedy simulation
* Reinforces substring search logic

## What This Problem Teaches

* Exponential growth through doubling
* Efficient brute-force with constraints
* Practical use of substring operations

## Key Takeaways

* Always exploit constraints to bound brute-force
* Check base cases before performing operations
* String doubling grows extremely fast

## Problem Difficulty Analysis

This is an **Easy-level** problem.

It relies on careful simulation and understanding of string growth, making it suitable for beginners and competitive programming warm-ups.
## 978B. File Name

## Platform

Codeforces

## Problem Link

[B. File Name](https://codeforces.com/problemset/problem/978/B)

## Problem Statement

You are given a file name represented as a string `s` of length `n`.

A file name is considered invalid if it contains **three or more consecutive `'x'` characters**.

Your task is to determine the **minimum number of characters that must be removed** so that the resulting string does not contain any occurrence of three consecutive `'x'` characters.

## Input Format

* The first line contains an integer `n`, the length of the string.
* The second line contains the string `s`.

## Output Format

* Print a single integer — the minimum number of characters that need to be removed.

## Constraints

* `3 ≤ n ≤ 100`
* `s` consists of lowercase English letters.

## Examples

### Example 1

Input

```text
6
xxxiii
```

Explanation

The string starts with:

```text
xxx
```

To avoid having three consecutive `'x'` characters, remove one `'x'`.

Result:

```text
xxiii
```

Output

```text
1
```

---

### Example 2

Input

```text
5
xxxxx
```

Explanation

```text
xxxxx
```

To leave at most two consecutive `'x'` characters:

```text
xxxxx → xx
```

Characters removed:

```text
3
```

Output

```text
3
```

---

### Example 3

Input

```text
9
xxixxxxxx
```

Explanation

The substring:

```text
xxxxxx
```

contains 6 consecutive `'x'`.

To reduce it to:

```text
xx
```

we remove:

```text
6 - 2 = 4
```

characters.

Output

```text
4
```

## Approach

Greedy Consecutive Character Counting

## Intuition

We only care about consecutive `'x'` characters.

For every continuous block of `'x'`:

```text
length = k
```

At most two `'x'` characters can remain.

Therefore:

```text
removals = k - 2
```

for every block where:

```text
k > 2
```

The provided solution counts consecutive `'x'` characters and increments the answer whenever the count exceeds `2`.

## Algorithm Steps

* Read `n` and string `s`.
* Initialize:

  * `r = 0` (current consecutive `'x'` count)
  * `ans = 0` (removals needed)
* Traverse the string:

  * If current character is `'x'`:

    * Increment `r`.
    * If `r > 2`, increment `ans`.
  * Otherwise:

    * Reset `r = 0`.
* Print `ans`.

## Visual Walkthrough

### Case 1

```text
s = "xxxiii"
```

Traversal:

```text
x → r=1
x → r=2
x → r=3 → ans=1
i → r=0
i → r=0
i → r=0
```

Answer:

```text
1
```

---

### Case 2

```text
s = "xxxxx"
```

Traversal:

```text
x → r=1
x → r=2
x → r=3 → ans=1
x → r=4 → ans=2
x → r=5 → ans=3
```

Answer:

```text
3
```

---

### Case 3

```text
s = "xxixxxxxx"
```

Traversal:

```text
x → r=1
x → r=2
i → r=0

x → r=1
x → r=2
x → r=3 → ans=1
x → r=4 → ans=2
x → r=5 → ans=3
x → r=6 → ans=4
```

Answer:

```text
4
```

## Complexity Analysis

### Time Complexity

**O(n)**

Each character is processed exactly once.

### Space Complexity

**O(1)**

Only a few integer variables are used.

## Solution Explanation

The solution maintains a counter `r` representing the current streak of consecutive `'x'` characters.

Whenever another `'x'` extends the streak beyond two:

```text
r > 2
```

that character must be removed in the optimal solution, so the answer is incremented.

Non-`'x'` characters break the streak and reset the counter.

This guarantees the minimum number of removals.

## Full Solution

### C++ Implementation

```cpp
#include<iostream>
using namespace std;

int main() {

    // Length of the string
    int n;

    // Input string
    string s;

    cin >> n >> s;

    // Current consecutive count of 'x'
    int r = 0;

    // Number of removals required
    int ans = 0;

    // Traverse the string
    for(char ch : s) {

        // Current character is 'x'
        if(ch == 'x') {

            // Increase consecutive count
            if(++r > 2) {

                // Any 'x' beyond the second one
                // must be removed
                ans++;
            }
        }
        else {

            // Reset streak
            r = 0;
        }
    }

    // Print minimum removals
    cout << ans << '\n';

    return 0;
}
```

## Test Cases Analysis

| String    | Consecutive x Blocks | Removals |
| --------- | -------------------- | -------- |
| xxxiii    | 3                    | 1        |
| xxxxx     | 5                    | 3        |
| xxixxxxxx | 2, 6                 | 4        |
| abcde     | 0                    | 0        |
| xx        | 2                    | 0        |

## Edge Cases to Consider

* No `'x'` characters in the string.
* Exactly two consecutive `'x'` characters.
* Entire string consists of `'x'`.
* Multiple separate `'x'` blocks.
* Minimum valid string length.

## Common Test Cases

* `"xxx"`
* `"xxxxx"`
* `"xx"`
* `"abcxxxdef"`
* `"xxxxxxxxxx"`

## Common Mistakes to Avoid

* Counting every `'x'` after the second block separately without tracking streaks.
* Forgetting to reset the consecutive counter on non-`'x'` characters.
* Removing two characters from `"xxx"` instead of one.

## Interview Relevance

* Tests greedy thinking.
* Demonstrates handling of consecutive-character constraints.
* Common string traversal pattern.

## What This Problem Teaches

* Consecutive character counting.
* Greedy removal strategies.
* Efficient single-pass string processing.

## Key Takeaways

* For any block of `k` consecutive `'x'` characters, exactly `k - 2` removals are needed.
* A running streak counter is sufficient.
* Many string problems can be solved with a single traversal.

## Problem Difficulty Analysis

This is an **Easy-level** problem.

The main observation is that only consecutive `'x'` blocks matter. Once identified, a simple linear scan efficiently computes the minimum number of removals required.
# A_LCM_Problem

## Platform

Codeforces

## Problem Link

[A. LCM Problem](https://codeforces.com/problemset/problem/1389/A)

## Problem Statement

You are given two integers `l` and `r`.

Your task is to find two integers `a` and `b` such that:

* `l ≤ a < b ≤ r`
* `LCM(a, b)` is equal to `b`

If such a pair exists, print `a` and `b`.
Otherwise, print:

```
-1 -1
```

---

## Input Format

* The first line contains an integer `t` — number of test cases.
* Each test case contains two integers `l` and `r`.

---

## Output Format

For each test case, print:

* Two integers `a` and `b` satisfying the condition, or
* `-1 -1` if no such pair exists.

---

## Constraints

* `1 ≤ t ≤ 10^4`
* `1 ≤ l < r ≤ 10^9`

---

## Examples

### Example 1

Input

```
3
1 10
3 5
6 9
```

Explanation

* For `1 10`:

  * Choose `(1, 2)`
  * `LCM(1,2) = 2` → valid
* For `3 5`:

  * Choose `(3, 6)` → invalid since 6 > 5
  * No valid pair exists → output `-1 -1`
* For `6 9`:

  * `2*l = 12 > 9` → no valid pair

Output

```
1 2
-1 -1
-1 -1
```

---

## Approach (Algorithm Type)

**Mathematical Observation with Greedy Construction**

---

## Intuition

We want:

```
LCM(a, b) = b
```

This condition holds when:

```
b is a multiple of a
```

Because:

```
LCM(a, b) = b  ⇔  b % a == 0
```

The simplest choice is:

```
a = l
b = 2*l
```

Now we just need to verify:

```
2*l ≤ r
```

If true:

* `(l, 2*l)` is a valid answer.

Otherwise:

* No such pair exists.

---

## Key Mathematical Insight

If `2*l > r`, then:

* The smallest possible multiple of `l` greater than `l` itself exceeds `r`.
* Therefore, no valid `b` exists in range.

Hence, the entire problem reduces to checking one condition.

---

## Algorithm Steps

* Read integer `t`.
* For each test case:

  * Read integers `l` and `r`.
  * If `2*l > r`:

    * Print `-1 -1`
  * Else:

    * Print `l` and `2*l`

---

## Visual Walkthrough

### Test Case 1

Input:

```
l = 2, r = 8
```

Check:

```
2*l = 4 ≤ 8 → valid
```

Pair:

```
(2, 4)
```

LCM:

```
LCM(2,4) = 4
```

Valid.

---

### Test Case 2

Input:

```
l = 5, r = 9
```

Check:

```
2*l = 10 > 9
```

No valid pair.

Output:

```
-1 -1
```

---

### Test Case 3

Input:

```
l = 3, r = 7
```

Check:

```
2*l = 6 ≤ 7
```

Pair:

```
(3, 6)
```

Valid.

---

## Complexity Analysis

### Time Complexity

For each test case:

* Only one comparison operation is performed.

Overall:

```
O(t)
```

---

### Space Complexity

```
O(1)
```

Only constant variables are used.

---

## Solution Explanation

The solution leverages a fundamental property of LCM:

If one number divides another, the LCM equals the larger number.

Thus:

* We attempt the smallest possible valid pair `(l, 2*l)`.
* If it lies within range, it is guaranteed correct.
* Otherwise, no solution exists.

This avoids brute-force searching entirely.

---

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

        int l, r;
        cin >> l >> r;

        // Check if double of l lies within range
        if(2 * l > r) {

            // No valid pair exists
            cout << "-1 -1\n";
        }
        else {

            // Valid pair found
            cout << l << ' ' << 2 * l << '\n';
        }
    }

    return 0;
}
```

---

## Test Cases Analysis

| l | r  | 2*l | Valid? | Output |
| - | -- | --- | ------ | ------ |
| 1 | 10 | 2   | Yes    | 1 2    |
| 3 | 5  | 6   | No     | -1 -1  |
| 6 | 12 | 12  | Yes    | 6 12   |
| 5 | 9  | 10  | No     | -1 -1  |

---

## Edge Cases to Consider

* Smallest possible range (`l + 1 = r`)
* `l = 1`
* `2*l = r`
* Maximum constraint values

---

## Common Test Cases

* Cases where solution exists
* Cases where no solution exists
* Large input values
* Edge boundaries

---

## Common Mistakes to Avoid

* Trying brute force over entire range
* Forgetting strict inequality `a < b`
* Overflow issues (if using larger constraints)

---

## Interview Relevance

* Tests understanding of LCM properties
* Emphasizes mathematical reduction of problems
* Encourages minimalistic logic

---

## What This Problem Teaches

* Recognizing divisibility patterns
* Leveraging number theory fundamentals
* Simplifying problems via observation

---

## Key Takeaways

* If `b` is a multiple of `a`, then `LCM(a, b) = b`.
* Always check the simplest valid candidate first.
* Many competitive programming problems reduce to one-line logic after insight.

---

## Problem Difficulty Analysis

This is an **Easy-level** problem on Codeforces.

It mainly tests basic number theory understanding and the ability to identify a direct mathematical shortcut instead of brute-force searching.
# A_Forbidden_Integer

## Platform

Codeforces

## Problem Link

[A. Forbidden Integer](https://codeforces.com/problemset/problem/1845/A)

## Problem Statement

You are given three integers:

* `n` — the required sum
* `k` — the maximum allowed integer value
* `x` — a **forbidden integer**

You must construct a sequence of integers such that:

* Each integer is between `1` and `k` inclusive.
* No element in the sequence equals `x`.
* The **sum of all integers equals `n`**.

If such a sequence exists:

* Print `"YES"`
* Print the length of the sequence
* Print the sequence itself.

If it is impossible, print `"NO"`.

## Input Format

* The first line contains an integer `t` — the number of test cases.
* Each test case contains three integers:

```
n k x
```

## Output Format

For each test case:

* Print `"YES"` and the valid sequence if possible.
* Otherwise print `"NO"`.

## Constraints

* `1 ≤ t ≤ 100`
* `1 ≤ n ≤ 100`
* `1 ≤ k ≤ 100`
* `1 ≤ x ≤ k`

## Examples

### Example 1

Input

```
3
5 2 1
6 3 1
4 2 2
```

Explanation

Test Case 1

```
n = 5
k = 2
x = 1
```

We cannot use `1`.

Allowed numbers:

```
2
```

But:

```
2 + 2 + 2 = 6
```

We cannot make sum `5`.

Output

```
NO
```

---

Test Case 2

```
n = 6
k = 3
x = 1
```

Allowed numbers:

```
2, 3
```

One valid solution:

```
2 + 2 + 2 = 6
```

Output

```
YES
3
2 2 2
```

---

Test Case 3

```
n = 4
k = 2
x = 2
```

Allowed numbers:

```
1
```

Solution:

```
1 + 1 + 1 + 1 = 4
```

Output

```
YES
4
1 1 1 1
```

## Approach

Case Analysis with Greedy Construction

## Intuition

The problem depends on whether `1` is forbidden.

### Case 1 — `x ≠ 1`

If `1` is allowed, the simplest solution is:

```
1 + 1 + 1 + ... + 1
```

`n` times.

This always produces sum `n`.

Thus:

```
length = n
sequence = n copies of 1
```

### Case 2 — `x = 1`

Now we **cannot use `1`**, so the smallest usable integer is `2`.

Two subcases arise.

#### Subcase A — `n` is even

We can construct:

```
2 + 2 + 2 + ...
```

Exactly:

```
n / 2 numbers
```

#### Subcase B — `n` is odd

We need one odd number to make the total odd.

If `k ≥ 3`, we can use:

```
3
```

Then fill the rest with `2`.

Example:

```
n = 7
3 + 2 + 2
```

If `k = 2`, we cannot use `3`.

Therefore the sum cannot be odd.

Result → impossible.

## Algorithm Steps

* Read integer `t`.

* For each test case:

  * Read `n`, `k`, `x`.

* If `x ≠ 1`:

  * Print `"YES"`
  * Print `n`
  * Print `n` copies of `1`.

* Else (`x = 1`):

  * If `k = 1`:

    * Print `"NO"`
  * Else if `n` is even:

    * Print `"YES"`
    * Print `n / 2`
    * Print `2` repeated `n / 2` times.
  * Else if `k ≥ 3`:

    * Print `"YES"`
    * Print `(n/2)`
    * Use `3` once and remaining `2`s.
  * Otherwise:

    * Print `"NO"`.

## Visual Walkthrough

### Test Case 1

Input

```
n = 6
k = 3
x = 1
```

Allowed numbers

```
2, 3
```

Construction

```
2 + 2 + 2
```

Sequence

```
[2,2,2]
```

---

### Test Case 2

Input

```
n = 7
k = 3
x = 1
```

Construction

```
3 + 2 + 2
```

Sequence

```
[2,2,3]
```

---

### Test Case 3

Input

```
n = 5
k = 2
x = 1
```

Allowed numbers

```
2
```

But

```
2 + 2 + 2 = 6
```

Impossible to get `5`.

Result

```
NO
```

## Complexity Analysis

### Time Complexity

```
O(n) per test case
```

Because we print at most `n` numbers.

### Space Complexity

```
O(1)
```

No extra memory structures are used.

## Solution Explanation

The code handles the two primary scenarios:

* When `1` is allowed → fill with `1`.
* When `1` is forbidden → use `2`s and possibly one `3`.

The condition

```
(!(n & 1) || k > 2)
```

ensures that either:

* `n` is even, or
* `3` is allowed (`k > 2`) for odd sums.

This guarantees the sum can be constructed.

## Full Solution

### C++ Implementation

```cpp
#include<iostream>
using namespace std;

int main() {

    int t, n, k, x;
    cin >> t;

    while(t--) {

        cin >> n >> k >> x;

        // Case when 1 is forbidden
        if(x == 1 && k != 1 && (!(n & 1) || k > 2)) {

            int len = n / 2;

            cout << "YES\n";
            cout << len << '\n';

            // Print 2's
            for(int i = 1; i < len; i++)
                cout << "2 ";

            // Last element
            if(n & 1)
                cout << "3\n";
            else
                cout << "2\n";
        }

        // Case when 1 is allowed
        else if(x != 1) {

            cout << "YES\n";
            cout << n << '\n';

            for(int i = 0; i < n; i++)
                cout << "1 ";

            cout << '\n';
        }

        // Impossible case
        else {
            cout << "NO\n";
        }
    }

    return 0;
}
```

## Test Cases Analysis

| n | k | x | Result  |
| - | - | - | ------- |
| 6 | 3 | 1 | 2 2 2   |
| 7 | 3 | 1 | 2 2 3   |
| 4 | 2 | 2 | 1 1 1 1 |
| 5 | 2 | 1 | NO      |

## Edge Cases to Consider

* `k = 1`
* `x = 1`
* `n` odd with `k = 2`
* `n = 1`

## Common Test Cases

```
5 2 1
6 3 1
7 3 1
4 2 2
```

## Common Mistakes to Avoid

* Forgetting that `1` may be forbidden
* Ignoring the odd `n` case
* Not checking if `3` is allowed when needed

## Interview Relevance

* Tests problem decomposition
* Demonstrates greedy construction
* Reinforces conditional reasoning

## What This Problem Teaches

* Handling constraints through case analysis
* Constructive algorithms
* Managing edge conditions carefully

## Key Takeaways

* Always check smallest possible building blocks
* Handle forbidden elements carefully
* Greedy constructions often solve sequence problems

## Problem Difficulty Analysis

This is an **Easy-level** problem.

The main challenge is recognizing the special case when `1` is forbidden and handling odd sums appropriately using `3`. Once the cases are identified, the implementation is straightforward.
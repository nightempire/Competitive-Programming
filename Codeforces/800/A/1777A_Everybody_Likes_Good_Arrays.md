## Platform

Codeforces

## Problem Link

[A. Everybody Likes Good Arrays](https://codeforces.com/problemset/problem/1777/A)

---

## Problem Statement

You are given an array `a` of size `n`.

An array is considered **good** if **no two adjacent elements have the same parity**, i.e.:

* Adjacent elements must alternate between **even** and **odd**

You can perform operations to remove elements from the array.

Your task is to determine the **minimum number of elements to remove** so that the array becomes **good**.

---

## Input Format

* The first line contains an integer `t` — number of test cases
* For each test case:

  * An integer `n`
  * An array of `n` integers

---

## Output Format

For each test case:

* Print a single integer — minimum number of removals

---

## Constraints

* `1 ≤ t ≤ 1000`
* `1 ≤ n ≤ 100`
* `1 ≤ a[i] ≤ 1000`

---

## Examples

### Example 1

Input

```id="1yx8lm"
3
5
1 2 3 4 5
4
2 4 6 8
3
1 3 5
```

Explanation

* Case 1:

  * Already alternating → no removals
* Case 2:

  * All even → remove 3 elements → keep one
* Case 3:

  * All odd → remove 2 elements

Output

```id="d7n4sa"
0
3
2
```

---

### Example 2

Input

```id="p3q7kl"
2
6
1 3 2 4 5 7
5
2 3 4 5 6
```

Explanation

* Count adjacent pairs with same parity

Output

```id="k5v2zr"
2
0
```

---

### Example 3

Input

```id="r8m2yd"
1
4
1 1 2 2
```

Explanation

* Adjacent same parity pairs:

  * (1,1) → same → remove 1
  * (2,2) → same → remove 1

Output

```id="a6z9jw"
2
```

---

## Approach

Greedy counting of adjacent parity conflicts

---

## Intuition

A **bad pair** occurs when:

```text id="y6q3zp"
parity(a[i]) == parity(a[i-1])
```

To fix each bad pair:

* We must remove **at least one element**

Thus, the minimum removals = **number of such bad adjacent pairs**

---

## Algorithm Steps

* Read `t`
* For each test case:

  * Read `n` and array `nums`
  * Initialize `ans = 0`
  * Loop from `i = 1` to `n-1`:

    * If parity of `nums[i]` equals parity of `nums[i-1]`:

      * Increment `ans`
  * Print `ans`

---

## Visual Walkthrough

### Case 1: `[1, 2, 3, 4, 5]`

```id="p6w4vh"
Odd → Even → Odd → Even → Odd
No conflicts → ans = 0
```

---

### Case 2: `[2, 4, 6, 8]`

```id="6m3z2r"
Even → Even → Even → Even

Conflicts:
(2,4), (4,6), (6,8) → 3
```

---

### Case 3: `[1, 1, 2, 2]`

```id="4b9s7x"
(1,1) → same → +1
(1,2) → different
(2,2) → same → +1

Total = 2
```

---

## Complexity Analysis

### Time Complexity

O(n) per test case

* Single traversal

---

### Space Complexity

O(1)

* No extra space required

---

## Solution Explanation

The solution identifies all adjacent pairs with the same parity.

Each such pair contributes one required removal, as at least one element must be deleted to break the parity conflict.

This greedy counting approach ensures minimum removals.

---

## Full Solution

### C++ Implementation

```cpp id="4n8wq1"
#include<iostream>
using namespace std;

int main() {

    // Number of test cases
    int t;
    cin >> t;

    while(t--) {

        // Size of array and answer
        int n, ans = 0;
        cin >> n;

        // Input array
        int nums[n];

        for(int i = 0; i < n; i++) {
            cin >> nums[i];
        }

        // Count adjacent pairs with same parity
        for(int i = 1; i < n; i++) {

            // Check parity using bitwise AND
            if((nums[i - 1] & 1) == (nums[i] & 1)) {

                // Same parity → conflict
                ans++;
            }
        }

        // Output result
        cout << ans << '\n';
    }

    return 0;
}
```

---

## Test Cases Analysis

| Array       | Conflicts | Output |
| ----------- | --------- | ------ |
| [1,2,3,4,5] | 0         | 0      |
| [2,4,6,8]   | 3         | 3      |
| [1,1,2,2]   | 2         | 2      |
| [1,3,5]     | 2         | 2      |

---

## Edge Cases to Consider

* Single element (`n = 1`)
* All even or all odd elements
* Already alternating arrays

---

## Common Test Cases

* Alternating parity → 0
* All same parity → n-1
* Mixed patterns

---

## Common Mistakes to Avoid

* Comparing values instead of parity
* Forgetting to check adjacent pairs only
* Overcomplicating with deletions simulation

---

## Interview Relevance

* Greedy thinking
* Pattern recognition
* Bitwise operations for parity

---

## What This Problem Teaches

* Simplifying problems using properties (parity)
* Counting instead of simulating operations
* Efficient traversal techniques

---

## Key Takeaways

* Count conflicts instead of fixing them explicitly
* Parity check can be done using `x & 1`
* Greedy counting yields optimal solution

---

## Problem Difficulty Analysis

This is an **Easy-level** problem.

It focuses on:

* Array traversal
* Greedy logic
* Basic bitwise operations
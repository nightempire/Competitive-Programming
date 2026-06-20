# A. Quintomania

## Platform

Codeforces

## Problem Link

[A. Quintomania - Codeforces Problem 2036A](https://codeforces.com/problemset/problem/2036/A?utm_source=chatgpt.com)

## Problem Statement

A sequence of musical notes is given.

For the sequence to be considered a valid **Quintomania** melody, the absolute difference between every pair of consecutive notes must be either:

* `5`, or
* `7`

For each test case, determine whether the given sequence satisfies this condition.

Print:

* `"YES"` if every consecutive pair differs by either `5` or `7`.
* `"NO"` otherwise.

## Input Format

* The first line contains an integer `t` — the number of test cases.
* For each test case:

  * The first line contains an integer `n` — the number of notes.
  * The second line contains `n` integers representing the sequence.

## Output Format

For each test case, print:

* `"YES"` if the sequence is a valid Quintomania melody.
* `"NO"` otherwise.

Each answer should be printed on a new line.

## Constraints

* `1 ≤ t ≤ 1000`
* `2 ≤ n ≤ 50`
* `-1000 ≤ ai ≤ 1000`

## Examples

### Example 1

Input

```text
1
4
10 15 22 27
```

Output

```text
YES
```

### Explanation

Differences:

```text
|15 - 10| = 5
|22 - 15| = 7
|27 - 22| = 5
```

All differences are either `5` or `7`.

Therefore:

```text
YES
```

---

### Example 2

Input

```text
1
3
1 6 14
```

Output

```text
NO
```

### Explanation

Differences:

```text
|6 - 1| = 5
|14 - 6| = 8
```

Since `8` is neither `5` nor `7`, the sequence is invalid.

Therefore:

```text
NO
```

---

### Example 3

Input

```text
1
5
20 13 18 11 16
```

Output

```text
YES
```

### Explanation

Differences:

```text
|13 - 20| = 7
|18 - 13| = 5
|11 - 18| = 7
|16 - 11| = 5
```

Every consecutive difference is valid.

Therefore:

```text
YES
```

## Approach

### Algorithm Type

Sequential Validation / Adjacent Difference Checking

## Intuition

The condition only depends on consecutive elements.

For every adjacent pair:

```text
ai, ai+1
```

compute:

```text
|ai+1 - ai|
```

If the difference is:

* `5` → valid
* `7` → valid

Otherwise, the sequence immediately becomes invalid.

Since each pair is checked exactly once, a simple linear scan is sufficient.

## Algorithm Steps

* Read the number of test cases `t`.
* For each test case:

  * Read `n`.
  * Read the first note.
  * Initialize a boolean variable `flag = true`.
  * For each remaining note:

    * Read the current note.
    * Compute:

```text
abs(current - previous)
```

```
* If the difference is neither `5` nor `7`:
  * Set `flag = false`.
* Update `previous = current`.
```

* Print:

  * `"YES"` if `flag` remains true.
  * `"NO"` otherwise.

## Visual Walkthrough

### Test Case 1

Sequence:

```text
10 15 22 27
```

Check differences:

```text
15 - 10 = 5 ✓
22 - 15 = 7 ✓
27 - 22 = 5 ✓
```

Result:

```text
YES
```

---

### Test Case 2

Sequence:

```text
1 6 14
```

Check differences:

```text
6 - 1 = 5 ✓
14 - 6 = 8 ✗
```

Invalid difference found.

Result:

```text
NO
```

---

### Test Case 3

Sequence:

```text
20 13 18 11 16
```

Check differences:

```text
|13 - 20| = 7 ✓
|18 - 13| = 5 ✓
|11 - 18| = 7 ✓
|16 - 11| = 5 ✓
```

All pairs satisfy the condition.

Result:

```text
YES
```

## Complexity Analysis

### Time Complexity

**O(n)** per test case

Each note is processed exactly once.

```text
Total checks = n - 1
```

Therefore:

```text
O(n)
```

### Space Complexity

**O(1)**

Only a few variables are maintained:

* `prev`
* `curr`
* `flag`

No extra data structures are required.

Therefore:

```text
O(1)
```

## Solution Explanation

The solution reads the sequence one element at a time.

For every newly read note:

* Compute the absolute difference from the previous note.
* Verify whether the difference equals `5` or `7`.
* If any difference violates the rule, mark the sequence as invalid.

After processing the entire sequence:

* Print `"YES"` if all adjacent differences were valid.
* Otherwise print `"NO"`.

This direct simulation exactly matches the problem requirements.

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

        // Number of notes
        int n;

        // Previous and current note values
        int prev, curr;

        cin >> n >> prev;

        // First note already read
        n--;

        // Assume sequence is valid initially
        bool flag = true;

        // Process remaining notes
        while(n--) {

            cin >> curr;

            // Calculate absolute difference
            int diff = abs(curr - prev);

            // Difference must be either 5 or 7
            if(flag && diff != 5 && diff != 7) {
                flag = false;
            }

            // Update previous note
            prev = curr;
        }

        // Print result
        cout << (flag ? "YES\n" : "NO\n");
    }

    return 0;
}
```

## Test Cases Analysis

| Sequence       | Consecutive Differences | Output |
| -------------- | ----------------------- | ------ |
| 10 15 22 27    | 5, 7, 5                 | YES    |
| 1 6 14         | 5, 8                    | NO     |
| 20 13 18 11 16 | 7, 5, 7, 5              | YES    |
| 5 10           | 5                       | YES    |
| 7 14           | 7                       | YES    |
| 1 9            | 8                       | NO     |

## Edge Cases to Consider

* Minimum sequence size (`n = 2`)
* All differences equal to `5`
* All differences equal to `7`
* Mixture of `5` and `7`
* First invalid difference occurring early
* Negative values in the sequence

## Common Test Cases

### Only Difference 5

```text
Input:
1
3
1 6 11

Output:
YES
```

---

### Only Difference 7

```text
Input:
1
3
10 17 24

Output:
YES
```

---

### Invalid Difference

```text
Input:
1
3
2 7 15

Output:
NO
```

---

### Mixed Valid Differences

```text
Input:
1
5
20 13 18 11 16

Output:
YES
```

## Common Mistakes to Avoid

* Forgetting to use the absolute value of the difference.
* Checking only for difference `5` and ignoring `7`.
* Comparing non-adjacent elements instead of consecutive elements.

## Interview Relevance

* Demonstrates sequential array validation.
* Tests careful implementation of adjacency conditions.
* Reinforces efficient one-pass traversal techniques.

## What This Problem Teaches

* Array traversal and validation.
* Using absolute differences effectively.
* Detecting violations during a single pass.

## Key Takeaways

* Consecutive-element problems often require only a linear scan.
* Early detection of invalid conditions simplifies implementation.
* Absolute differences are useful when direction does not matter.

## Problem Difficulty Analysis

This is an **Easy** implementation problem.

The solution requires only checking whether every adjacent pair satisfies a fixed condition. No advanced algorithms or data structures are necessary, making it a straightforward one-pass validation task.
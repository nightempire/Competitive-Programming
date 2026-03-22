# A_Most_Unstable_Array

## Platform

Codeforces

## Problem Link

[A. Most Unstable Array](https://codeforces.com/problemset/problem/1353/A)

## Problem Statement

You are given two integers:

* `n` — the size of the array
* `m` — the maximum possible value for any element in the array

You need to construct an array of size `n` such that:

* Each element is between `0` and `m`
* The **sum of absolute differences between consecutive elements** is maximized

Formally, maximize:

```text
|a1 - a2| + |a2 - a3| + ... + |a(n-1) - a(n)|
```

## Input Format

* The first line contains an integer `t` — number of test cases.
* Each test case contains two integers:

```text
n m
```

## Output Format

For each test case, print the **maximum possible sum of absolute differences**.

## Constraints

* `1 ≤ t ≤ 1000`
* `1 ≤ n ≤ 100`
* `0 ≤ m ≤ 100`

## Examples

### Example 1

Input

```
3
1 5
2 3
3 4
```

Explanation

Case 1:

```
n = 1
```

No adjacent elements → sum = `0`

---

Case 2:

```
n = 2
```

Best choice:

```
[0, m] → difference = m
```

---

Case 3:

```
n = 3
```

Best choice:

```
[0, m, 0]
```

Differences:

```
|0 - m| + |m - 0| = m + m = 2m
```

Output

```
0
3
8
```

## Approach

Greedy Construction Based on Extremes

## Intuition

To maximize:

```text
|a[i] - a[i+1]|
```

we should maximize the difference between consecutive elements.

The maximum possible difference is:

```text
m
```

(by choosing `0` and `m`).

### Cases

#### Case 1 — `n = 1`

No adjacent elements:

```
Answer = 0
```

---

#### Case 2 — `n = 2`

Only one difference:

```
Answer = m
```

---

#### Case 3 — `n ≥ 3`

We can alternate between `0` and `m`:

```
[0, m, 0, m, ...]
```

Each adjacent pair contributes `m`.

Total pairs:

```
n - 1
```

But maximum sum stabilizes at:

```
2m
```

Because:

```
|0 - m| + |m - 0| = 2m
```

Further additions don’t increase the maximum beyond this pattern.

## Algorithm Steps

* Read integer `t`
* For each test case:

  * Read `n`, `m`
  * If `n == 1` → print `0`
  * Else if `n == 2` → print `m`
  * Else → print `2 * m`

## Visual Walkthrough

### Case 1

```
n = 1, m = 5
```

Array:

```
[5]
```

No differences:

```
0
```

---

### Case 2

```
n = 2, m = 3
```

Array:

```
[0, 3]
```

Difference:

```
3
```

---

### Case 3

```
n = 4, m = 4
```

Array:

```
[0, 4, 0, 4]
```

Differences:

```
4 + 4 + 4 = 12
```

But maximum optimal strategy yields:

```
2 * m = 8
```

## Complexity Analysis

### Time Complexity

```
O(t)
```

Each test case is handled in constant time.

### Space Complexity

```
O(1)
```

No extra space required.

## Solution Explanation

The solution uses simple case-based logic:

* For `n = 1`, no adjacent difference exists.
* For `n = 2`, only one difference → `m`.
* For `n ≥ 3`, alternating extremes gives maximum → `2m`.

This avoids constructing the array explicitly.

## Full Solution

### C++ Implementation

```cpp
#include<iostream>
using namespace std;

int main() {

    int t, n, m;
    cin >> t;

    while(t--) {

        cin >> n >> m;

        // Case 1: single element
        if(n == 1)
            cout << "0\n";

        // Case 2: two elements
        else if(n == 2)
            cout << m << '\n';

        // Case 3: three or more elements
        else
            cout << 2 * m << '\n';
    }

    return 0;
}
```

## Test Cases Analysis

| n | m  | Result |
| - | -- | ------ |
| 1 | 5  | 0      |
| 2 | 3  | 3      |
| 3 | 4  | 8      |
| 4 | 10 | 20     |

## Edge Cases to Consider

* `n = 1`
* `m = 0`
* `n = 2`
* Large number of test cases

## Common Test Cases

```
1 10
2 5
3 7
4 0
```

## Common Mistakes to Avoid

* Overthinking for `n ≥ 3`
* Trying to construct full array unnecessarily
* Missing edge case `n = 1`

## Interview Relevance

* Tests pattern recognition
* Demonstrates greedy thinking
* Emphasizes simplifying problems

## What This Problem Teaches

* Identifying optimal patterns
* Avoiding brute force construction
* Using case-based reasoning

## Key Takeaways

* Maximum difference comes from extremes (`0` and `m`)
* Small cases often define the general pattern
* Mathematical observation simplifies implementation

## Problem Difficulty Analysis

This is an **Easy-level** problem.

The main challenge is recognizing the pattern for different values of `n`. Once identified, the solution becomes a simple conditional check.
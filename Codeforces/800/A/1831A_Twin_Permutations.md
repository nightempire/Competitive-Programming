# A_Twin_Permutations

## Platform

Codeforces

## Problem Link

[A. Twin Permutations](https://codeforces.com/problemset/problem/1831/A)

## Problem Statement

You are given a **permutation** `p` of size `n`.

A permutation is an array containing all integers from `1` to `n` exactly once.

Your task is to construct another permutation `q` such that:

```text
p[i] + q[i] = n + 1   for all i
```

In other words, for every index `i`, the sum of elements at that position in both permutations must equal `n + 1`.

## Input Format

* The first line contains an integer `t` — the number of test cases.
* For each test case:

  * The first line contains an integer `n`.
  * The second line contains `n` integers representing permutation `p`.

## Output Format

For each test case, print `n` integers — the permutation `q`.

## Constraints

* `1 ≤ t ≤ 1000`
* `1 ≤ n ≤ 100`
* `1 ≤ p[i] ≤ n`
* `p` is a valid permutation

## Examples

### Example 1

Input

```
1
5
1 2 3 4 5
```

Explanation

We need:

```
p[i] + q[i] = 6
```

So:

| p[i] | q[i] |
| ---- | ---- |
| 1    | 5    |
| 2    | 4    |
| 3    | 3    |
| 4    | 2    |
| 5    | 1    |

Output

```
5 4 3 2 1
```

---

### Example 2

Input

```
1
4
2 1 4 3
```

Explanation

```
n + 1 = 5
```

| p[i] | q[i] |
| ---- | ---- |
| 2    | 3    |
| 1    | 4    |
| 4    | 1    |
| 3    | 2    |

Output

```
3 4 1 2
```

---

### Example 3

Input

```
1
3
3 1 2
```

Explanation

```
n + 1 = 4
```

| p[i] | q[i] |
| ---- | ---- |
| 3    | 1    |
| 1    | 3    |
| 2    | 2    |

Output

```
1 3 2
```

## Approach

Direct Complement Construction

## Intuition

We are given:

```
p[i] + q[i] = n + 1
```

Rearranging:

```
q[i] = n + 1 - p[i]
```

Thus, for each element:

* Compute its complement relative to `n + 1`.

This guarantees:

* Each value lies between `1` and `n`
* All values are unique (since `p` is a permutation)

Hence, `q` is also a valid permutation.

## Algorithm Steps

* Read integer `t`.
* For each test case:

  * Read `n`.
  * For each element `p[i]`:

    * Compute:

```
q[i] = n - p[i] + 1
```

* Print all values of `q`.

## Visual Walkthrough

### Test Case 1

Input

```
p = [1, 2, 3, 4, 5]
n = 5
```

Compute:

```
q[i] = 6 - p[i]
```

Result:

```
[5, 4, 3, 2, 1]
```

---

### Test Case 2

```
p = [2, 1, 4, 3]
n = 4
```

Compute:

```
q = [3, 4, 1, 2]
```

---

### Test Case 3

```
p = [3, 1, 2]
n = 3
```

Compute:

```
q = [1, 3, 2]
```

## Complexity Analysis

### Time Complexity

```
O(n) per test case
```

Each element is processed once.

### Space Complexity

```
O(n)
```

To store the resulting permutation.

## Solution Explanation

The solution constructs the required permutation directly using a mathematical formula.

For each element in the given permutation:

```
q[i] = n - p[i] + 1
```

This ensures:

* The sum condition is satisfied
* The result is a valid permutation

The program uses fast I/O for efficiency.

## Full Solution

### C++ Implementation

```cpp
#include<iostream>
using namespace std;

int main() {

    int t;
    cin >> t;

    while(t--) {

        int n;
        cin >> n;

        // Array to store result permutation
        int nums[n];

        for(int i = 0; i < n; i++) {

            int num;
            cin >> num;

            // Compute complement
            nums[i] = n - num + 1;
        }

        // Output result permutation
        for(int num : nums)
            cout << num << ' ';

        cout << '\n';
    }

    return 0;
}
```

## Test Cases Analysis

| p         | n | q         |
| --------- | - | --------- |
| 1 2 3 4 5 | 5 | 5 4 3 2 1 |
| 2 1 4 3   | 4 | 3 4 1 2   |
| 3 1 2     | 3 | 1 3 2     |

## Edge Cases to Consider

* `n = 1`
* Reverse permutation
* Random permutation
* Minimum constraints

## Common Test Cases

```
1
1
1

1
5
5 4 3 2 1
```

## Common Mistakes to Avoid

* Using incorrect formula (`n - p[i]` instead of `n - p[i] + 1`)
* Forgetting that permutation starts from `1`
* Not handling multiple test cases properly

## Interview Relevance

* Demonstrates permutation manipulation
* Tests understanding of transformations
* Encourages direct mathematical solutions

## What This Problem Teaches

* Complement-based transformations
* Properties of permutations
* Efficient array construction

## Key Takeaways

* Simple formulas can solve permutation problems
* Always verify constraints for validity
* Direct construction is often optimal

## Problem Difficulty Analysis

This is an **Easy-level** problem.

It mainly requires recognizing the direct relationship between `p[i]` and `q[i]`, after which implementation is straightforward.

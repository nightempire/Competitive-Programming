## Platform

Codeforces

## Problem Link

[C. Advantage](https://codeforces.com/problemset/problem/1760/C)

---

## Problem Statement

You are given an array `a` of size `n`.

For each element `a[i]`, compute its **advantage**, defined as:

* The difference between `a[i]` and the **maximum element among all other elements**

Formally:

```text
advantage[i] = a[i] - max(a[j]) for all j ≠ i
```

You must output the advantage for each element.

---

## Input Format

* The first line contains an integer `t` — number of test cases
* For each test case:

  * An integer `n`
  * An array of `n` integers

---

## Output Format

For each test case:

* Print `n` integers — the advantage values

---

## Constraints

* `1 ≤ t ≤ 10^4`
* `2 ≤ n ≤ 2 × 10^5`
* `1 ≤ a[i] ≤ 10^9`
* Sum of all `n` across test cases ≤ `2 × 10^5`

---

## Examples

### Example 1

Input

```
1
5
1 2 3 4 5
```

Explanation

* Max = 5, Second max = 4

Output

```
-4 -3 -2 -1 1
```

---

### Example 2

Input

```
1
4
7 7 7 7
```

Explanation

* All elements equal → max = 7, second max = 7

Output

```
0 0 0 0
```

---

### Example 3

Input

```
1
3
10 5 8
```

Explanation

* Max = 10, Second max = 8

Output

```
2 -5 -2
```

---

## Approach

Greedy with maximum and second maximum tracking

---

## Intuition

For each element:

* If it is **not the maximum**, subtract the **maximum**
* If it is the **maximum**, subtract the **second maximum**

This ensures:

* We always compare against the largest *other* element

---

## Algorithm Steps

* Read `t`
* For each test case:

  * Read `n` and array `nums`
  * Find:

    * Maximum (`mx`)
    * Second maximum (`smx`)
  * Traverse array:

    * If `num == mx`:

      * Print `num - smx`
    * Else:

      * Print `num - mx`

---

## Visual Walkthrough

### Case 1: `[1, 2, 3, 4, 5]`

```
mx = 5, smx = 4

1 → 1 - 5 = -4
2 → 2 - 5 = -3
3 → 3 - 5 = -2
4 → 4 - 5 = -1
5 → 5 - 4 = 1
```

---

### Case 2: `[7, 7, 7, 7]`

```
mx = 7, smx = 7

All → 7 - 7 = 0
```

---

### Case 3: `[10, 5, 8]`

```
mx = 10, smx = 8

10 → 10 - 8 = 2
5  → 5 - 10 = -5
8  → 8 - 10 = -2
```

---

## Complexity Analysis

### Time Complexity

O(n) per test case

* One pass to find max and second max
* One pass to compute results

---

### Space Complexity

O(1)

* No extra space apart from variables

---

## Solution Explanation

The solution avoids recomputing maximum for each element by:

* Precomputing the largest and second largest values
* Using them to efficiently calculate each advantage

This ensures optimal performance even for large inputs.

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

        // Size of array
        int n;
        cin >> n;

        // Input array
        int nums[n];

        for(int i = 0; i < n; i++) {
            cin >> nums[i];
        }

        // Variables to store maximum and second maximum
        int mx = 0, smx = 0;

        // Find maximum and second maximum
        for(int num : nums) {

            if(num > mx) {
                smx = mx;
                mx = num;
            }
            else if(num > smx) {
                smx = num;
            }
        }

        // Compute advantage for each element
        for(int num : nums) {

            if(num != mx) {
                cout << num - mx << ' ';
            }
            else {
                cout << num - smx << ' ';
            }
        }

        cout << '\n';
    }

    return 0;
}
```

---

## Test Cases Analysis

| Array       | Max | Second Max | Output        |
| ----------- | --- | ---------- | ------------- |
| [1,2,3,4,5] | 5   | 4          | -4 -3 -2 -1 1 |
| [7,7,7,7]   | 7   | 7          | 0 0 0 0       |
| [10,5,8]    | 10  | 8          | 2 -5 -2       |

---

## Edge Cases to Consider

* All elements equal
* Only two elements
* Large values
* Multiple occurrences of maximum

---

## Common Test Cases

* Increasing sequence
* All equal values
* Random order values

---

## Common Mistakes to Avoid

* Not handling multiple max elements properly
* Incorrect second maximum calculation
* Recomputing max repeatedly (inefficient)

---

## Interview Relevance

* Greedy optimization
* Efficient array traversal
* Handling edge cases in maximum problems

---

## What This Problem Teaches

* Importance of precomputing values
* Handling multiple maxima
* Writing optimal linear solutions

---

## Key Takeaways

* Use second maximum when excluding max
* Avoid redundant computations
* Single-pass solutions are powerful

---

## Problem Difficulty Analysis

This is an **Easy-level** problem.

It focuses on:

* Array manipulation
* Greedy logic
* Efficient computation
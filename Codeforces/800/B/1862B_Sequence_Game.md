# B_Sequence_Game

## Platform

Codeforces

## Problem Link

[B. Sequence Game](https://codeforces.com/problemset/problem/1862/B)

## Problem Statement

You are given a sequence of integers.

You must construct a new sequence following this rule:

* Start with the first element of the given sequence.
* For every next element:

  * If the current element is **greater than or equal to** the previous element in the constructed sequence, append it **once**.
  * Otherwise, append the current element **twice**.

After processing all elements, output:

* The length of the constructed sequence
* The constructed sequence itself

## Input Format

* The first line contains an integer `t`, the number of test cases
* For each test case:

  * An integer `n`, the length of the original sequence
  * `n` integers representing the sequence

## Output Format

* For each test case:

  * Print an integer — the length of the constructed sequence
  * Print the elements of the constructed sequence

## Constraints

* `1 ≤ t ≤ 10^4`
* `1 ≤ n ≤ 50`
* `1 ≤ ai ≤ 1000`

## Examples

### Example 1

Input

```
1
4
1 3 2 4
```

Explanation

Construction process:

* Start with `1` → `[1]`
* `3 ≥ 1` → append once → `[1, 3]`
* `2 < 3` → append twice → `[1, 3, 2, 2]`
* `4 ≥ 2` → append once → `[1, 3, 2, 2, 4]`

Output

```
5
1 3 2 2 4
```

---

### Example 2

Input

```
1
3
5 5 5
```

Explanation

All elements are non-decreasing:

```
[5] → [5, 5] → [5, 5, 5]
```

Output

```
3
5 5 5
```

---

### Example 3

Input

```
1
3
5 3 1
```

Explanation

Every new element is smaller than the previous:

```
[5]
[5, 3, 3]
[5, 3, 3, 1, 1]
```

Output

```
5
5 3 3 1 1
```

## Approach

**Greedy Construction Using Previous Element Comparison**

## Intuition

The rule depends only on the comparison between:

* The current input element
* The last element added to the result sequence

This allows a greedy approach:

* Decide immediately how many times to append the current element
* No future elements affect the current decision

## Algorithm Steps

* Read the number of test cases `t`
* For each test case:

  * Read `n`
  * Read the first element and add it to the result sequence
  * For each remaining element:

    * If current element ≥ last element of result:

      * Append it once
    * Else:

      * Append it twice
  * Output the size of the result sequence
  * Output the result sequence

## Visual Walkthrough

### Case 1: `1 3 2 4`

```
Start: [1]
3 ≥ 1 → [1, 3]
2 < 3 → [1, 3, 2, 2]
4 ≥ 2 → [1, 3, 2, 2, 4]
```

---

### Case 2: `5 3`

```
Start: [5]
3 < 5 → [5, 3, 3]
```

---

### Case 3: `2 2 1`

```
[2]
2 ≥ 2 → [2, 2]
1 < 2 → [2, 2, 1, 1]
```

## Complexity Analysis

### Time Complexity

**O(n)** per test case

Each element is processed once with constant-time operations.

### Space Complexity

**O(n)**

The result sequence may grow up to `2n` elements in the worst case.

## Solution Explanation

The solution builds the required sequence step by step.

At each step, it compares the current element with the last inserted element:

* If the sequence remains non-decreasing, one insertion is sufficient
* If the sequence decreases, duplicating the current element preserves the required structure

This direct greedy construction matches the problem rules exactly.

## Full Solution

### C++ Implementation

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {

    int t;
    cin >> t;

    while (t--) {

        int n;
        cin >> n;

        vector<int> res;

        int curr;
        cin >> curr;

        // Add the first element
        res.push_back(curr);
        n--;

        // Process remaining elements
        while (n--) {

            cin >> curr;

            // If current element is non-decreasing
            if (curr >= res.back()) {
                res.push_back(curr);
            } else {
                // If decreasing, add twice
                res.push_back(curr);
                res.push_back(curr);
            }
        }

        // Output result
        cout << res.size() << '\n';
        for (int x : res) {
            cout << x << ' ';
        }
        cout << '\n';
    }

    return 0;
}
```

## Test Cases Analysis

| Input Sequence | Result Sequence | Size |
| -------------- | --------------- | ---- |
| `1 3 2 4`      | `1 3 2 2 4`     | 5    |
| `5 5 5`        | `5 5 5`         | 3    |
| `5 3 1`        | `5 3 3 1 1`     | 5    |

## Edge Cases to Consider

* `n = 1`
* Strictly increasing sequence
* Strictly decreasing sequence
* All equal elements

## Common Test Cases

* Mixed increasing and decreasing patterns
* Small input sizes
* Multiple test cases

## Common Mistakes to Avoid

* Comparing with the previous input instead of last result element
* Forgetting to print the sequence size
* Incorrect handling of the first element

## Interview Relevance

* Tests greedy thinking
* Evaluates sequence construction logic
* Reinforces careful condition handling

## What This Problem Teaches

* Greedy decision-making
* Importance of using constructed state instead of raw input
* Clean simulation of rules

## Key Takeaways

* Local comparisons can drive global construction
* Greedy strategies are effective when rules are simple
* Always compare with the actual sequence state

## Problem Difficulty Analysis

This is an **Easy-level** problem.

The logic is straightforward, but careful adherence to the construction rules is essential to avoid incorrect results.
# B_ICPC_Balloons

## Platform

Codeforces

## Problem Link

[B. ICPC Balloons](https://codeforces.com/problemset/problem/1703/B)

## Problem Statement

During an ICPC contest, a team solves problems represented by uppercase English letters.

For each solved problem:

* The team receives **one balloon** for solving it.
* If the problem is solved **for the first time**, they receive **one extra balloon** as a bonus.

Your task is to calculate the **total number of balloons** received by the team based on the sequence of solved problems.

Each test case is independent.

## Input Format

* The first line contains an integer `t`, the number of test cases.
* For each test case:

  * An integer `n`, the number of solved problems.
  * A string `s` of length `n`, consisting of uppercase English letters (`A` to `Z`).

## Output Format

* For each test case, print a single integer representing the total number of balloons.

## Constraints

* `1 ≤ t ≤ 1000`
* `1 ≤ n ≤ 50`
* `s[i] ∈ {'A' … 'Z'}`

## Examples

### Example 1

Input

```
1
3
ABA
```

Explanation

* First `A` → first time → 2 balloons
* `B` → first time → 2 balloons
* Second `A` → already solved → 1 balloon

Total balloons:

```
2 + 2 + 1 = 5
```

Output

```
5
```

---

### Example 2

Input

```
1
5
ABCDE
```

Explanation

* Each problem is solved for the first time
* Each contributes `2` balloons

Total balloons:

```
5 × 2 = 10
```

Output

```
10
```

## Approach

**Frequency Tracking Using Boolean Array**

## Intuition

Every solved problem gives **at least one balloon**.

If a problem is solved for the **first time**, it gives **one additional balloon**.

So:

* First occurrence of a character → `2` balloons
* Repeated occurrence → `1` balloon

Tracking whether a problem has been solved before allows accurate counting.

## Algorithm Steps

* Read number of test cases `t`.
* For each test case:

  * Read integer `n` and string `s`.
  * Initialize a boolean array of size `26` to track solved problems.
  * Initialize `balloons = 0`.
  * For each character in `s`:

    * If the problem is not yet solved:

      * Increment `balloons` once for the bonus.
      * Mark it as solved.
    * Increment `balloons` once for solving the problem.
  * Output the total balloon count.

## Visual Walkthrough

### Test Case: `s = "ABA"`

Step-by-step:

```
A → first time → +2 balloons (total = 2)
B → first time → +2 balloons (total = 4)
A → already solved → +1 balloon  (total = 5)
```

Final Answer:

```
5
```

---

### Test Case: `s = "AAB"`

```
A → first time → +2 (total = 2)
A → repeat     → +1 (total = 3)
B → first time → +2 (total = 5)
```

## Complexity Analysis

### Time Complexity

**O(n) per test case**

* Each character in the string is processed once.

### Space Complexity

**O(1)**

* Fixed-size boolean array of size 26.

## Solution Explanation

The solution uses a boolean array to track whether a problem has already been solved.
Each character contributes one balloon by default, and an additional balloon if it appears for the first time.

This method is efficient, simple, and perfectly matches the problem rules.

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

        int n, balloons = 0;
        cin >> n;

        string s;
        cin >> s;

        // Boolean array to track if a problem is already solved
        bool vis[26] = {0};

        // Process each solved problem
        for (char ch : s) {

            // If this problem is solved for the first time
            if (!vis[ch - 'A']) {
                balloons++;               // Bonus balloon
                vis[ch - 'A'] = true;     // Mark as solved
            }

            balloons++; // Balloon for solving the problem
        }

        // Output total balloons
        cout << balloons << '\n';
    }

    return 0;
}
```

## Test Cases Analysis

| Input String | Unique Problems | Total Balloons |
| ------------ | --------------- | -------------- |
| `A`          | 1               | 2              |
| `AA`         | 1               | 3              |
| `AB`         | 2               | 4              |
| `ABA`        | 2               | 5              |
| `ABCDE`      | 5               | 10             |

## Edge Cases to Consider

* All characters are the same
* All characters are unique
* Minimum length string (`n = 1`)

## Common Test Cases

* Repeated problem patterns
* Sequential unique problems
* Mixed repetitions

## Common Mistakes to Avoid

* Forgetting the extra balloon for first-time problems
* Incorrect indexing for character mapping
* Not resetting tracking array per test case

## Interview Relevance

* Tests basic frequency tracking
* Reinforces conditional logic
* Demonstrates efficient use of constant memory

## What This Problem Teaches

* Handling uniqueness in sequences
* Translating rules into counting logic
* Efficient state tracking with arrays

## Key Takeaways

* First-time events often require special handling
* Boolean arrays are effective for fixed alphabets
* Clear logic prevents overcounting or undercounting

## Problem Difficulty Analysis

This is an **Easy-level** problem.
It focuses on observation and correct counting rather than complex algorithms.
# B_Ten_Words_of_Wisdom

## Platform

Codeforces

## Problem Link

[B. Ten Words of Wisdom](https://codeforces.com/problemset/problem/1850/B)

## Problem Statement

Monocarp is organizing a competition. There are `n` participants, and each participant submits a solution characterized by two integers:

* `a` → the number of words in the solution.
* `b` → the quality score of the solution.

Monocarp will only consider solutions with **at most 10 words** (`a ≤ 10`). Among those valid solutions, he wants to select the one with the **maximum quality score**.

Your task is to determine the **index (1-based)** of the participant whose solution will be selected.

If multiple participants have the same highest quality score among valid ones, select the one with the smallest index.

---

## Input Format

* The first line contains an integer `t` — number of test cases.
* For each test case:

  * The first line contains an integer `n` — number of participants.
  * The next `n` lines each contain two integers:

    * `a` — number of words.
    * `b` — quality score.

---

## Output Format

For each test case, print a single integer — the **1-based index** of the selected participant.

---

## Constraints

* `1 ≤ t ≤ 100`
* `1 ≤ n ≤ 50`
* `1 ≤ a ≤ 100`
* `1 ≤ b ≤ 100`

---

## Examples

### Example 1

Input

```
1
4
12 5
8 9
10 7
9 6
```

Explanation

Participants:

* Participant 1 → `a = 12` → invalid (more than 10 words)
* Participant 2 → `a = 8`, `b = 9` → valid
* Participant 3 → `a = 10`, `b = 7` → valid
* Participant 4 → `a = 9`, `b = 6` → valid

Among valid ones, maximum quality is `9` (Participant 2).

Output

```
2
```

---

### Example 2

Input

```
1
3
15 100
20 90
5 80
```

Explanation

* Participant 1 → invalid
* Participant 2 → invalid
* Participant 3 → valid with quality 80

Output

```
3
```

---

### Example 3

Input

```
1
5
9 5
10 5
8 5
7 5
6 5
```

Explanation

All are valid and have equal quality.
The first occurrence with maximum quality is selected.

Output

```
1
```

---

## Approach (Algorithm Type)

**Linear Scan with Conditional Filtering and Maximum Tracking**

---

## Intuition

Each participant is evaluated independently.

We only care about:

* Solutions with `a ≤ 10`
* Among them, the maximum `b`

This naturally suggests iterating through all participants, filtering valid ones, and maintaining the current maximum quality and its corresponding index.

---

## Algorithm Steps

* Read integer `t`.
* For each test case:

  * Read integer `n`.
  * Initialize:

    * `mx = 0` (maximum quality found so far)
    * `idx = 0` (index of best participant)
  * Iterate from `i = 1` to `n`:

    * Read `a` and `b`.
    * If `a > 10`, skip.
    * If `b > mx`:

      * Update `mx = b`
      * Update `idx = i`
  * Print `idx`.

---

## Visual Walkthrough

### Test Case 1

Input:

```
4
12 5
8 9
10 7
9 6
```

Processing:

| i | a  | b | Valid (a ≤ 10)? | mx | idx |
| - | -- | - | --------------- | -- | --- |
| 1 | 12 | 5 | No              | 0  | 0   |
| 2 | 8  | 9 | Yes             | 9  | 2   |
| 3 | 10 | 7 | Yes             | 9  | 2   |
| 4 | 9  | 6 | Yes             | 9  | 2   |

Final answer → **2**

---

### Test Case 2

Input:

```
3
15 100
20 90
5 80
```

Only third participant is valid.

Result → **3**

---

### Test Case 3

Input:

```
5
9 5
10 5
8 5
7 5
6 5
```

All valid, same quality.

First occurrence retained → **1**

---

## Complexity Analysis

### Time Complexity

**O(n) per test case**

* Each participant is processed exactly once.
* For `t` test cases → O(t × n).

---

### Space Complexity

**O(1)**

* Only constant variables (`mx`, `idx`) are used.
* No extra data structures.

---

## Solution Explanation

The solution iterates through each participant while maintaining:

* A running maximum quality score (`mx`)
* The corresponding index (`idx`)

If a participant exceeds the word limit (`a > 10`), they are ignored.
Otherwise, their quality score is compared with the current maximum.
If higher, both `mx` and `idx` are updated.

This ensures:

* Only valid entries are considered.
* The first occurrence of maximum quality is selected.

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

        // Number of participants
        int n;

        // mx -> stores maximum quality found so far
        // idx -> stores index (1-based) of best participant
        int mx = 0, idx = 0;

        cin >> n;

        // Iterate through all participants
        for(int i = 1; i <= n; i++) {

            int a, b;

            // a -> number of words
            // b -> quality score
            cin >> a >> b;

            // Skip participants with more than 10 words
            if(a > 10)
                continue;

            // If current quality is higher than maximum found
            if(b > mx) {

                // Update maximum quality
                mx = b;

                // Store current index
                idx = i;
            }
        }

        // Output the index of best participant
        cout << idx << '\n';
    }

    return 0;
}
```

---

## Test Cases Analysis

| Test Case       | Valid Participants | Max Quality | Output                     |
| --------------- | ------------------ | ----------- | -------------------------- |
| All invalid     | None               | 0           | 0 (if constraints allowed) |
| Single valid    | One                | That value  | Index                      |
| Multiple valid  | Many               | Highest b   | First occurrence           |
| Equal qualities | All equal          | Same        | Smallest index             |

---

## Edge Cases to Consider

* All participants have `a > 10`
* Only one participant
* Multiple participants with same highest quality
* Maximum constraints (`n = 50`, `t = 100`)

---

## Common Test Cases

* Mixed valid and invalid participants
* Exactly one valid participant
* All participants valid
* All participants invalid

---

## Common Mistakes to Avoid

* Forgetting 1-based indexing
* Not resetting `mx` and `idx` for each test case
* Incorrectly handling tie-breaking logic

---

## Interview Relevance

* Demonstrates filtering with conditions
* Shows maximum tracking pattern
* Tests attention to indexing rules

---

## What This Problem Teaches

* Conditional filtering during iteration
* Maintaining running maximum
* Careful reading of constraints

---

## Key Takeaways

* Linear scanning is often sufficient for small constraints.
* Always apply filtering conditions before comparison.
* Maintain clear separation between validation and evaluation logic.

---

## Problem Difficulty Analysis

This is an **Easy-level** problem on Codeforces.

It focuses on:

* Basic iteration
* Conditional filtering
* Maximum tracking

Suitable for beginners and as a warm-up for competitive programming contests.

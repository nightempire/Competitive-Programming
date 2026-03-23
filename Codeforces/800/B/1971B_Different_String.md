## Platform

Codeforces

## Problem Link

[B. Different String](https://codeforces.com/problemset/problem/1971/B)

---

## Problem Statement

You are given a string `s` consisting of lowercase English letters.

Your task is to determine whether it is possible to rearrange the string such that **no two adjacent characters are the same**.

If possible, output **"YES"** and one such rearranged string.
Otherwise, output **"NO"**.

---

## Input Format

* The first line contains an integer `t` — the number of test cases.
* Each test case consists of a single string `s`.

---

## Output Format

For each test case:

* Print `"YES"` followed by a valid rearranged string, if possible.
* Otherwise, print `"NO"`.

---

## Constraints

* `1 ≤ t ≤ 1000`
* `1 ≤ |s| ≤ 100`
* `s` consists only of lowercase English letters

---

## Examples

### Example 1

Input

```
3
abba
aaaa
abc
```

Explanation

* `abba` → Swap adjacent different characters → valid
* `aaaa` → All characters same → impossible
* `abc` → Already valid

Output

```
YES
baba
NO
YES
bac
```

---

### Example 2

Input

```
2
zz
az
```

Explanation

* `zz` → All characters same → impossible
* `az` → Already valid

Output

```
NO
YES
za
```

---

### Example 3

Input

```
1
aab
```

Explanation

* Swap adjacent unequal characters → valid arrangement exists

Output

```
YES
aba
```

---

## Approach

Greedy adjacent swap strategy

---

## Intuition

If all characters in the string are identical, then no rearrangement can avoid adjacent duplicates.

Otherwise, as soon as we find **two consecutive different characters**, we can swap them to break any uniform pattern and ensure a valid configuration.

This works because:

* We only need **one valid rearrangement**
* A single swap of unequal adjacent characters guarantees a different structure

---

## Algorithm Steps

* Read number of test cases `t`
* For each test case:

  * Read string `s`
  * Traverse the string from index `1` to `n-1`
  * If `s[i] != s[i-1]`:

    * Swap `s[i]` and `s[i-1]`
    * Print `"YES"` and modified string
    * Stop further processing
  * If no such pair is found:

    * Print `"NO"`

---

## Visual Walkthrough

### Case 1: `abba`

```
a b b a
  ↑ ↑
Different characters found → swap

Result:
b a b a
```

---

### Case 2: `aaaa`

```
a a a a
All characters identical → no swap possible
```

---

### Case 3: `abc`

```
a b c
  ↑ ↑
Swap → b a c
```

---

## Complexity Analysis

### Time Complexity

O(n) per test case

* We traverse the string once to find the first unequal adjacent pair.

---

### Space Complexity

O(1)

* Only in-place swapping is performed.
* No additional data structures are used.

---

## Solution Explanation

The solution efficiently checks whether a valid rearrangement is possible by identifying any adjacent unequal pair.

If found, swapping them guarantees a different arrangement that avoids uniform adjacency. If no such pair exists, it implies all characters are identical, making it impossible to construct a valid string.

This greedy approach is optimal and avoids unnecessary complexity.

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

    // Process each test case
    while(t--) {

        // Input string
        string s;
        cin >> s;

        // Length of the string
        int n = s.length();

        // Flag to check if rearrangement is possible
        bool flag = true;

        // Traverse the string to find first unequal adjacent pair
        for(int i = 1; i < n; i++) {

            // If current and previous characters are different
            if(s[i - 1] != s[i]) {

                // Swap them
                char temp = s[i - 1];
                s[i - 1] = s[i];
                s[i] = temp;

                // Output result
                cout << "YES\n" << s << '\n';

                // Mark as successful
                flag = false;

                // Stop further processing
                break;
            }
        }

        // If no valid swap found → all characters same
        if(flag) {
            cout << "NO\n";
        }
    }

    return 0;
}
```

---

## Test Cases Analysis

| Input String | Condition           | Output |
| ------------ | ------------------- | ------ |
| `aaaa`       | All characters same | NO     |
| `ab`         | Adjacent different  | YES    |
| `abba`       | Mixed characters    | YES    |
| `z`          | Single character    | NO     |
| `abcde`      | All unique          | YES    |

---

## Edge Cases to Consider

* String of length `1`
* All characters identical
* Already valid strings
* Strings with only one differing pair

---

## Common Test Cases

* `aaaa` → NO
* `abab` → YES
* `zzzzzz` → NO
* `abacaba` → YES

---

## Common Mistakes to Avoid

* Not checking all characters before deciding `"NO"`
* Incorrect swapping indices
* Printing result without breaking loop

---

## Interview Relevance

* Tests greedy thinking
* Evaluates string manipulation skills
* Highlights early-exit optimization

---

## What This Problem Teaches

* Identifying simple patterns in strings
* Using greedy logic for quick solutions
* Importance of early termination

---

## Key Takeaways

* If all characters are identical → impossible case
* One valid rearrangement is sufficient
* Simple swaps can solve structural problems efficiently

---

## Problem Difficulty Analysis

This is an **Easy-level** problem.

It focuses on:

* Basic string traversal
* Conditional logic
* Greedy strategy

Ideal for beginners and quick practice.
# A_Spell_Check

## Platform

Codeforces

## Problem Link

[A. Spell Check](https://codeforces.com/problemset/problem/1722/A)

## Problem Statement

You are given a string consisting of lowercase English letters.

Your task is to determine whether the string can be **rearranged** to form the word:

```
Timur
```

The check is **case-sensitive**, and the string must contain **exactly five characters**.

Each test case is independent.

## Input Format

* The first line contains an integer `t`, the number of test cases.
* For each test case:

  * An integer `n`, the length of the string.
  * A string `s` of length `n`.

## Output Format

* For each test case:

  * Print `YES` if the string can be rearranged to form `"Timur"`.
  * Otherwise, print `NO`.

## Constraints

* `1 ≤ t ≤ 1000`
* `1 ≤ n ≤ 10`
* `s` contains only lowercase English letters

## Examples

### Example 1

Input

```
3
5
Timur
5
miTur
4
Timu
```

Explanation

* `"Timur"` → already matches → valid
* `"miTur"` → rearranged to `"Timur"` → valid
* `"Timu"` → incorrect length → invalid

Output

```
YES
YES
NO
```

---

### Example 2

Input

```
1
5
rumiT
```

Explanation

* Rearranging `"rumiT"` gives `"Timur"`

Output

```
YES
```

## Approach

**Sorting-Based String Comparison**

## Intuition

Since the order of characters does not matter, we can:

* Sort the input string
* Sort the target word `"Timur"`
* Compare both results

If they match and the string length is exactly 5, the spell is valid.

## Algorithm Steps

* Read number of test cases `t`.
* For each test case:

  * Read integer `n` and string `s`.
  * If `n != 5`, print `NO` and continue.
  * Sort string `s`.
  * Compare it with the sorted version of `"Timur"`.
  * Print `YES` if equal, otherwise `NO`.

## Visual Walkthrough

### Test Case 1: `s = "miTur"`

Before sorting:

```
m i T u r
```

After sorting:

```
T i m r u
```

Sorted target:

```
T i m r u
```

Result:

```
Match → YES
```

---

### Test Case 2: `s = "Timu"`

* Length ≠ 5
* Immediately invalid

Result:

```
NO
```

## Complexity Analysis

### Time Complexity

**O(n log n)** per test case

* Sorting the string of fixed size (5 characters).

### Space Complexity

**O(1)**

* Sorting is done in-place.
* Constant extra memory.

## Solution Explanation

The solution validates the string length first to eliminate impossible cases early.
Sorting allows a direct comparison with the target word regardless of character order.

This approach is simple, reliable, and efficient for small fixed-size strings.

## Full Solution

### C++ Implementation

```cpp
#include <iostream>
#include <algorithm>
using namespace std;

int main() {

    // Number of test cases
    int t;
    cin >> t;

    while (t--) {

        int n;
        cin >> n;

        string s;
        cin >> s;

        // If length is not exactly 5, it cannot form "Timur"
        if (n != 5) {
            cout << "NO\n";
            continue;
        }

        // Sort the string to allow comparison regardless of order
        sort(s.begin(), s.end());

        // Compare with sorted version of "Timur"
        cout << (s == "Timru" ? "YES\n" : "NO\n");
    }

    return 0;
}
```

## Test Cases Analysis

| Input String | Length | Rearrangement Possible | Output |
| ------------ | ------ | ---------------------- | ------ |
| `Timur`      | 5      | Yes                    | YES    |
| `miTur`      | 5      | Yes                    | YES    |
| `rumiT`      | 5      | Yes                    | YES    |
| `Timu`       | 4      | No                     | NO     |
| `Timurr`     | 6      | No                     | NO     |

## Edge Cases to Consider

* Incorrect string length
* Repeated characters
* Missing required characters

## Common Test Cases

* Permutations of `"Timur"`
* Strings with extra characters
* Strings with fewer than five characters

## Common Mistakes to Avoid

* Ignoring the length constraint
* Comparing unsorted strings
* Case mismatches

## Interview Relevance

* Tests string manipulation
* Demonstrates sorting-based comparison
* Reinforces constraint-based validation

## What This Problem Teaches

* Importance of early constraint checks
* Efficient handling of permutations
* Clean string comparison techniques

## Key Takeaways

* Sorting simplifies permutation checks
* Fixed-size problems often allow elegant solutions
* Validate constraints before computation

## Problem Difficulty Analysis

This is an **Easy-level** problem.
It emphasizes logical validation and basic string operations rather than algorithmic complexity.
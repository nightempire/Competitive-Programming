# B_Your_Name

## Platform

Codeforces

## Problem Link

[B. Your Name](https://codeforces.com/problemset/problem/2167/B)

## Problem Statement

You are given two strings `s` and `t`, both of length `n`.

Your task is to determine whether the two strings contain exactly the same multiset of characters.

In other words, check if `t` is a permutation (an anagram) of `s`.

If both strings contain the same characters with the same frequencies, print:

```
YES
```

Otherwise, print:

```
NO
```

---

## Input Format

* The first line contains an integer `q` — number of test cases.
* For each test case:

  * An integer `n` — length of the strings.
  * A string `s`.
  * A string `t`.

---

## Output Format

For each test case, print:

* `YES` if `s` and `t` are anagrams.
* `NO` otherwise.

---

## Constraints

* `1 ≤ q ≤ 10^4`
* `1 ≤ n ≤ 2 × 10^5`
* Strings consist of lowercase English letters.
* The sum of all `n` across test cases does not exceed `2 × 10^5`.

---

## Examples

### Example 1

Input

```
3
3
abc
cba
4
abcd
abce
5
hello
llheo
```

Explanation

* `abc` and `cba` → same letters → YES
* `abcd` and `abce` → different letters → NO
* `hello` and `llheo` → same letters → YES

Output

```
YES
NO
YES
```

---

## Approach (Algorithm Type)

**Frequency Counting (Character Hashing Technique)**

---

## Intuition

Two strings are anagrams if and only if:

* They contain exactly the same characters.
* Each character appears the same number of times in both strings.

Since only lowercase English letters are involved, we can use a frequency array of size 26.

Plan:

* Count frequencies of characters in `s`.
* Subtract frequencies using characters from `t`.
* If all counts return to zero → strings are identical in frequency.

---

## Algorithm Steps

* Read integer `q`.
* For each test case:

  * Read integer `n`.
  * Read strings `s` and `t`.
  * Initialize an integer array `f[26]` with zeros.
  * For each character in `s`, increment corresponding frequency.
  * For each character in `t`, decrement corresponding frequency.
  * If all elements in `f` are zero:

    * Print `YES`
  * Otherwise:

    * Print `NO`

---

## Visual Walkthrough

### Test Case 1

Input:

```
s = abc
t = cba
```

Frequency updates:

After `s`:

```
a:1 b:1 c:1
```

After `t`:

```
a:0 b:0 c:0
```

All zero → **YES**

---

### Test Case 2

Input:

```
s = abcd
t = abce
```

After `s`:

```
a:1 b:1 c:1 d:1
```

After `t`:

```
a:0 b:0 c:0 d:1 e:-1
```

Non-zero values exist → **NO**

---

### Test Case 3

Input:

```
s = hello
t = llheo
```

After `s`:

```
h:1 e:1 l:2 o:1
```

After `t`:

```
h:0 e:0 l:0 o:0
```

All zero → **YES**

---

## Complexity Analysis

### Time Complexity

For each test case:

* Traversing `s` → O(n)
* Traversing `t` → O(n)
* Checking 26 elements → O(1)

Overall:

```
O(total n across all test cases)
```

Since total `n ≤ 2 × 10^5`, the solution is efficient.

---

### Space Complexity

```
O(1)
```

Only a fixed-size array of length 26 is used.

---

## Solution Explanation

The solution uses a character frequency difference array.

By:

* Incrementing counts for `s`
* Decrementing counts for `t`

If both strings have identical frequency distributions, every index in the frequency array becomes zero.

If any index is non-zero, the strings differ.

This approach avoids sorting and works in linear time.

---

## Full Solution

### C++ Implementation

```cpp
#include<iostream>
using namespace std;

int main() {

    // Number of test cases
    int q;
    cin >> q;

    while(q--) {

        int n;
        cin >> n;

        string s, t;
        cin >> s >> t;

        // Frequency array for 26 lowercase letters
        int f[26] = {0};

        // Count characters in string s
        for(char ch : s) {
            f[ch - 'a']++;
        }

        // Subtract characters using string t
        for(char ch : t) {
            f[ch - 'a']--;
        }

        // Check if all frequencies are zero
        bool flag = false;
        for(int i : f) {
            if(i != 0) {
                flag = true;
                break;
            }
        }

        // If any mismatch found, print NO
        // otherwise print YES
        cout << (flag ? "NO\n" : "YES\n");
    }

    return 0;
}
```

---

## Test Cases Analysis

| s     | t     | Result |
| ----- | ----- | ------ |
| abc   | cba   | YES    |
| abcd  | abce  | NO     |
| hello | llheo | YES    |
| aaaa  | aaab  | NO     |
| z     | z     | YES    |

---

## Edge Cases to Consider

* Single character strings
* Completely different characters
* Repeated characters
* Large input size (performance check)

---

## Common Test Cases

* Identical strings
* One character difference
* Reordered characters
* All characters same

---

## Common Mistakes to Avoid

* Forgetting to reset frequency array for each test case
* Using sorting (O(n log n)) unnecessarily
* Ignoring constraint that total length is large

---

## Interview Relevance

* Classic anagram checking problem
* Tests understanding of hashing and frequency counting
* Common in string manipulation interviews

---

## What This Problem Teaches

* Efficient character counting
* Avoiding unnecessary sorting
* Handling multiple test cases correctly

---

## Key Takeaways

* Two strings are anagrams if their character frequencies match.
* Frequency arrays provide O(n) solution.
* Always exploit constraints (only lowercase letters).

---

## Problem Difficulty Analysis

This is an **Easy-level** Codeforces problem.

It primarily tests string manipulation and frequency counting, making it a foundational problem for beginners in competitive programming.
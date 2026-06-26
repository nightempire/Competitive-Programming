# A. Recovering a Small String

## Platform

Codeforces

## Problem Link

[A. Recovering a Small String - Codeforces Problem 1931A](https://codeforces.com/problemset/problem/1931/A?utm_source=chatgpt.com)

## Problem Statement

You are given an integer `n`.

Your task is to construct the **lexicographically smallest** string of length **3** consisting only of lowercase English letters such that the sum of the alphabetical positions of its characters equals `n`.

The alphabetical positions are:

```text
a = 1
b = 2
...
z = 26
```

Print the required string for each test case.

## Input Format

* The first line contains an integer `t` — the number of test cases.
* Each of the next `t` lines contains a single integer `n`.

## Output Format

For each test case, print the lexicographically smallest valid string of length `3`.

## Constraints

* `1 ≤ t ≤ 100`
* `3 ≤ n ≤ 78`

Since:

* Minimum possible sum = `1 + 1 + 1 = 3`
* Maximum possible sum = `26 + 26 + 26 = 78`

## Examples

### Example 1

Input

```text
3
3
6
30
```

Output

```text
aaa
aad
acz
```

### Explanation

#### Test Case 1

Required sum:

```text
3
```

Smallest possible string:

```text
a + a + a
1 + 1 + 1 = 3
```

Output:

```text
aaa
```

---

#### Test Case 2

Required sum:

```text
6
```

Lexicographically smallest valid string:

```text
a + a + d
1 + 1 + 4 = 6
```

Output:

```text
aad
```

---

#### Test Case 3

Required sum:

```text
30
```

Lexicographically smallest valid string:

```text
a + c + z
1 + 3 + 26 = 30
```

Output:

```text
acz
```

## Approach

### Algorithm Type

Brute Force Enumeration (Lexicographical Search)

## Intuition

There are only **26** lowercase letters.

The solution checks every possible string of length `3` in lexicographical order:

```text
aaa
aab
aac
...
zzz
```

The first string whose character-value sum equals `n` is automatically the lexicographically smallest valid answer.

Since:

```text
26³ = 17,576
```

possible strings exist, a brute-force search is fast enough.

## Algorithm Steps

* Read the number of test cases `t`.
* For each test case:

  * Read `n`.
  * Iterate over the first character from `'a'` to `'z'`.
  * Iterate over the second character from `'a'` to `'z'`.
  * Iterate over the third character from `'a'` to `'z'`.
  * Compute:

```text
(first value) + (second value) + (third value)
```

* If the sum equals `n`:

  * Print the string.
  * Stop searching for the current test case.

## Visual Walkthrough

### Test Case 1

Input:

```text
n = 6
```

Search order:

```text
aaa → sum = 3
aab → sum = 4
aac → sum = 5
aad → sum = 6 ✓
```

First valid string:

```text
aad
```

---

### Test Case 2

Input:

```text
n = 30
```

Search progression:

```text
aaa
aab
...
acy
acz ✓
```

Character values:

```text
a = 1
c = 3
z = 26
```

Sum:

```text
1 + 3 + 26 = 30
```

Output:

```text
acz
```

---

### Test Case 3

Input:

```text
n = 78
```

Only possible combination:

```text
z + z + z
26 + 26 + 26 = 78
```

Output:

```text
zzz
```

## Complexity Analysis

### Time Complexity

The algorithm checks at most:

```text
26 × 26 × 26 = 17,576
```

combinations.

Therefore:

```text
O(26³)
```

Since `26` is a constant, this is effectively:

```text
O(1)
```

per test case.

### Space Complexity

**O(1)**

Only a few loop variables and a boolean flag are used.

No additional data structures are required.

## Solution Explanation

The solution generates every possible three-letter lowercase string in lexicographical order.

For each generated string, it computes the sum of the alphabetical positions of its characters.

Whenever the sum equals the required value `n`, the string is immediately printed.

Because the search is performed in lexicographical order, the first valid string found is guaranteed to be the lexicographically smallest answer.

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

        // Required alphabetical sum
        int n;
        cin >> n;

        // Indicates whether a valid string has been found
        bool flag = false;

        // Try every possible first character
        for(int i = 0; i < 26; i++) {

            // Try every possible second character
            for(int j = 0; j < 26; j++) {

                // Try every possible third character
                for(int k = 0; k < 26; k++) {

                    // Alphabet values are:
                    // a = 1, b = 2, ..., z = 26
                    if(i + j + k + 3 == n) {

                        // Print the lexicographically smallest valid string
                        cout << (char)('a' + i)
                             << (char)('a' + j)
                             << (char)('a' + k)
                             << '\n';

                        flag = true;
                        break;
                    }
                }

                // Stop searching once the answer is found
                if(flag) break;
            }

            if(flag) break;
        }
    }

    return 0;
}
```

## Test Cases Analysis

| Input `n` | First Valid String | Character Values | Output |
| --------- | ------------------ | ---------------- | ------ |
| 3         | aaa                | 1 + 1 + 1        | aaa    |
| 6         | aad                | 1 + 1 + 4        | aad    |
| 30        | acz                | 1 + 3 + 26       | acz    |
| 52        | ayz                | 1 + 25 + 26      | ayz    |
| 78        | zzz                | 26 + 26 + 26     | zzz    |

## Edge Cases to Consider

* Minimum possible sum (`n = 3`)
* Maximum possible sum (`n = 78`)
* Sum requiring repeated characters
* Sum requiring all different characters
* Only one valid lexicographically smallest answer

## Common Test Cases

### Minimum Sum

```text
Input:
1
3

Output:
aaa
```

---

### Maximum Sum

```text
Input:
1
78

Output:
zzz
```

---

### Middle Value

```text
Input:
1
30

Output:
acz
```

---

### Repeated Characters

```text
Input:
1
6

Output:
aad
```

## Common Mistakes to Avoid

* Forgetting that letter values start from `1` rather than `0`.
* Continuing the search after finding the first valid string, which may print multiple answers.
* Ignoring lexicographical order when generating candidate strings.

## Interview Relevance

* Demonstrates brute-force enumeration over a small search space.
* Tests understanding of lexicographical ordering.
* Reinforces the idea that brute force is acceptable when the search space is sufficiently small.

## What This Problem Teaches

* Lexicographical traversal of combinations.
* Mapping characters to numerical values.
* Recognizing when constant-size brute force is an efficient solution.

## Key Takeaways

* A bounded search space often makes brute-force solutions practical.
* Traversing candidates in lexicographical order naturally yields the smallest valid answer.
* Character-to-number conversions are common in string manipulation problems.

## Problem Difficulty Analysis

This is an **Easy** brute-force implementation problem.

The key observation is that there are only **17,576** possible three-letter lowercase strings. Enumerating them in lexicographical order guarantees that the first string matching the required sum is the correct answer, resulting in a simple and efficient constant-time solution.
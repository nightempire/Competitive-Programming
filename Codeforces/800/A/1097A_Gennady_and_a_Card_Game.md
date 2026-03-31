## Platform

Codeforces

## Problem Link

[A. Gennady and a Card Game](https://codeforces.com/problemset/problem/1097/A)

---

## Problem Statement

Gennady is playing a card game.

He has one card in his hand, and there are **five cards on the table**.

Each card is represented by a string of length 2:

* First character → **rank** (`A, 2, 3, ..., 9, T, J, Q, K`)
* Second character → **suit** (`S, H, D, C`)

Gennady can play his card if:

* The **rank matches**, OR
* The **suit matches**

Determine whether Gennady can play his card.

---

## Input Format

* First line: string `s1` — Gennady’s card
* Next 5 lines: strings `s2` — cards on the table

---

## Output Format

* Print `"YES"` if Gennady can play
* Otherwise print `"NO"`

---

## Constraints

* Each card is a valid 2-character string
* Exactly 5 table cards are given

---

## Examples

### Example 1

Input:

```id="p9b3mz"
AS
AH
2D
3C
4S
5H
```

Explanation

* Gennady’s card: `AS`
* Table contains `AH` → same rank (`A`)

Output

```id="e5j2z1"
YES
```

---

### Example 2

Input

```id="k2n4vl"
KH
2D
3C
4S
5H
6D
```

Explanation

* `KH` matches `5H` → same suit (`H`)

Output

```id="r8y6tx"
YES
```

---

### Example 3

Input

```id="m7q2ea"
9D
AS
KH
QC
JD
TS
```

Explanation

* No rank or suit matches

Output

```id="t2k7hv"
NO
```

---

## Approach

Simple matching (linear scan)

---

## Intuition

We only need to check whether **any one of the five cards** matches Gennady’s card.

Matching condition:

```id="9a1z8v"
Same rank OR same suit
```

Since there are only 5 cards, a simple loop is sufficient.

---

## Algorithm Steps

* Read Gennady’s card `s1`
* Loop 5 times:

  * Read table card `s2`
  * If:

    * `s1[0] == s2[0]` (rank match) OR
    * `s1[1] == s2[1]` (suit match)
    * → print `"YES"` and terminate
* If no match found → print `"NO"`

---

## Visual Walkthrough

### Case 1

```id="f3k8nz"
s1 = AS
table = AH

Rank matches → YES
```

---

### Case 2

```id="v4r2xm"
s1 = KH
table = 5H

Suit matches → YES
```

---

### Case 3

```id="u7m1qp"
s1 = 9D
table = AS, KH, QC, JD, TS

No match → NO
```

---

## Complexity Analysis

### Time Complexity

O(1)

* Always checks exactly 5 cards

---

### Space Complexity

O(1)

* Only a few variables used

---

## Solution Explanation

The solution performs a straightforward scan through the 5 table cards.

At each step, it checks whether either:

* The **rank matches**, or
* The **suit matches**

If any match is found, the answer is immediately `"YES"`.

Otherwise, after checking all cards, the answer is `"NO"`.

---

## Full Solution

### C++ Implementation

```cpp id="7n3c2v"
#include<iostream>
using namespace std;

int main() {

    // Gennady's card
    string s1;

    // Table card
    string s2;

    // Read Gennady's card
    cin >> s1;

    // Check all 5 table cards
    for(int i = 0; i < 5; i++) {

        cin >> s2;

        // Check if rank OR suit matches
        if(s1[0] == s2[0] || s1[1] == s2[1]) {

            // Valid move found
            cout << "YES\n";

            // Exit early
            return 0;
        }
    }

    // No matching card found
    cout << "NO\n";

    return 0;
}
```

---

## Test Cases Analysis

| s1 | Table Cards        | Match Type | Output |
| -- | ------------------ | ---------- | ------ |
| AS | AH, 2D, 3C, 4S, 5H | Rank       | YES    |
| KH | 2D, 3C, 4S, 5H, 6D | Suit       | YES    |
| 9D | AS, KH, QC, JD, TS | None       | NO     |

---

## Edge Cases to Consider

* Match occurs on first card
* Match occurs on last card
* No matches at all
* All cards same suit or rank

---

## Common Test Cases

* Same rank → YES
* Same suit → YES
* No match → NO

---

## Common Mistakes to Avoid

* Checking only rank or only suit
* Not exiting early after finding match
* Incorrect indexing of string characters

---

## Interview Relevance

* Basic string handling
* Conditional logic
* Early termination optimization

---

## What This Problem Teaches

* Efficient scanning
* Pattern matching in small datasets
* Writing clean and simple logic

---

## Key Takeaways

* Check minimal conditions directly
* Use early exit for efficiency
* Keep logic simple when constraints are small

---

## Problem Difficulty Analysis

This is an **Easy-level** problem.

It focuses on:

* String comparison
* Basic logic
* Input handling
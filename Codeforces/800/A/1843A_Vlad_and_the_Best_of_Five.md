# A_Vlad_and_the_Best_of_Five

## Platform

Codeforces

## Problem Link

[A. Vlad and the Best of Five](https://codeforces.com/problemset/problem/1843/A)

## Problem Statement

Vlad is watching a competitive match consisting of **five games** between two players, **A** and **B**.
Each game has a winner, represented by a character:

* `'A'` → Player A wins the game
* `'B'` → Player B wins the game

The winner of the match is the player who wins **strictly more than half** of the five games.

Given the results of multiple matches, determine the overall winner for each match.

## Input Format

* The first line contains an integer `t`, the number of test cases.
* Each test case contains a single string `s` of length `5`.

  * Each character in `s` is either `'A'` or `'B'`.

## Output Format

For each test case, print:

* `'A'` if player A wins the match
* `'B'` otherwise

Each result should be printed on a new line.

## Constraints

* `1 ≤ t ≤ 1000`
* `|s| = 5`
* `s[i] ∈ {'A', 'B'}`

## Examples

### Example 1

Input

```
3
AABBA
AAAAA
BBABB
```

Explanation

* Match 1: A wins 3 games, B wins 2 games → A wins the match
* Match 2: A wins all 5 games → A wins the match
* Match 3: B wins 3 games, A wins 2 games → B wins the match

Output

```
A
A
B
```

### Example 2

Input

```
2
ABBBA
ABBBB
```

Explanation

* Match 1: A wins 2 games → not enough to win → B wins
* Match 2: A wins 1 game → B wins

Output

```
B
B
```

## Approach

**Frequency Counting / Majority Decision Algorithm**

## Intuition

Each match has exactly **five games**, so a player must win **at least three games** to be declared the winner.

Instead of tracking both players, it is sufficient to:

* Count how many times `'A'` appears in the string
* If A wins more than 2 games, A is the winner
* Otherwise, B is the winner

This keeps the logic minimal, efficient, and easy to reason about.

## Algorithm Steps

* Read the number of test cases `t`
* For each test case:

  * Read the string `s`
  * Initialize a counter for player A’s wins
  * Traverse the string and increment the counter whenever `'A'` appears
  * If the counter is greater than 2:

    * Print `'A'`
  * Otherwise:

    * Print `'B'`

## Visual Walkthrough

### Test Case 1

Input string:

```
A A B B A
```

Count of `'A'`:

```
3
```

Decision:

```
3 > 2 → Winner is A
```

---

### Test Case 2

Input string:

```
B B A B B
```

Count of `'A'`:

```
1
```

Decision:

```
1 ≤ 2 → Winner is B
```

---

### Test Case 3

Input string:

```
A A A A A
```

Count of `'A'`:

```
5
```

Decision:

```
5 > 2 → Winner is A
```

## Complexity Analysis

### Time Complexity

**O(t)**

Each test case processes exactly 5 characters, which is constant time.
Overall complexity scales linearly with the number of test cases.

### Space Complexity

**O(1)**

Only a few integer variables are used.
No extra data structures are required.

## Solution Explanation

The solution relies on the observation that winning a majority of five games requires at least three wins. By counting how many times player A appears as the winner, we can directly determine the match winner. This avoids unnecessary comparisons and keeps the solution concise and efficient.

## Full Solution

### C++ Implementation

```cpp
#include <iostream>
using namespace std;

int main() {

    // Number of test cases
    int t;
    cin >> t;

    // Process each test case independently
    while (t--) {

        // String representing results of 5 games
        // Each character is either 'A' or 'B'
        string s;
        cin >> s;

        // Counter to store number of games won by player A
        int countA = 0;

        // Traverse the result string
        for (char ch : s) {

            // If player A won this game, increment counter
            if (ch == 'A') {
                countA++;
            }
        }

        // Player A must win strictly more than half (i.e., at least 3 games)
        if (countA > 2) {
            cout << "A\n";
        } else {
            cout << "B\n";
        }
    }

    return 0;
}
```

## Test Cases Analysis

| Test Case Input | Count of A | Expected Output |
| --------------- | ---------- | --------------- |
| `AABBA`         | 3          | A               |
| `ABBBA`         | 1          | B               |
| `AAAAA`         | 5          | A               |
| `BBBBB`         | 0          | B               |
| `ABABA`         | 3          | A               |

## Edge Cases to Consider

* Player A wins exactly 3 games
* Player A wins 0 games
* All games won by the same player
* Maximum number of test cases

## Common Test Cases

* Mixed results with close scores
* Dominant wins by one player
* Alternating win patterns

## Common Mistakes to Avoid

* Using `>= 2` instead of `> 2`
* Forgetting that the string length is always 5
* Mishandling multiple test cases

## Interview Relevance

* Demonstrates majority-element logic
* Tests string traversal and counting
* Common pattern in decision-based problems

## What This Problem Teaches

* How to apply majority rules cleanly
* Efficient string processing
* Writing concise conditional logic

## Key Takeaways

* Fixed-size input enables simple and fast solutions
* Counting is often more effective than simulation
* Clear problem constraints simplify design choices

## Problem Difficulty Analysis

This is an **Easy-level** problem.
It focuses on basic counting, condition checking, and input handling, making it suitable for beginners and interview warm-up practice.
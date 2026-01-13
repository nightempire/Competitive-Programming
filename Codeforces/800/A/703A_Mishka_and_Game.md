# A_Mishka_and_Game

## Platform

Codeforces

## Problem Link

[A. Mishka and Game](https://codeforces.com/problemset/problem/703/A)

## Problem Statement

Mishka and Chris are playing a game consisting of multiple rounds.

In each round:

* Mishka scores `a` points
* Chris scores `b` points

The winner of a round is the player with the **higher score**.
If both players score the same, the round is considered a **draw**.

After all rounds are played, determine:

* `"Mishka"` if Mishka wins more rounds
* `"Chris"` if Chris wins more rounds
* `"Friendship is magic!^^"` if both win the same number of rounds

## Input Format

* The first line contains an integer `n`, the number of rounds.
* The next `n` lines each contain two integers `a` and `b`.

## Output Format

Print a single line containing the result of the game.

## Constraints

* `1 ≤ n ≤ 100`
* `0 ≤ a, b ≤ 100`

## Examples

### Example 1

Input

```
3
3 5
2 1
4 4
```

Explanation

* Round 1 → Chris wins
* Round 2 → Mishka wins
* Round 3 → Draw

Total wins

```
Mishka = 1
Chris = 1
```

Result

```
Friendship is magic!^^
```

Output

```
Friendship is magic!^^
```

### Example 2

Input

```
2
5 3
6 2
```

Explanation

Mishka wins both rounds.

Output

```
Mishka
```

## Approach (Algorithm Name / Type)

**Score Comparison with Counting**

## Intuition

Each round is independent.

By comparing the scores round by round and keeping track of how many rounds each player wins, the final winner can be decided with a simple comparison of total wins.

Draw rounds do not affect the final outcome.

## Algorithm Steps

* Read the number of rounds `n`
* Initialize counters for Mishka and Chris
* For each round:

  * Read scores `a` and `b`
  * Increment Mishka’s counter if `a > b`
  * Increment Chris’s counter if `a < b`
* Compare both counters and print the appropriate result

## Visual Walkthrough

### Test Case 1

Rounds

```
(3,5) → Chris wins
(2,1) → Mishka wins
(4,4) → Draw
```

Win counts

```
Mishka = 1
Chris = 1
```

Final Result

```
Friendship is magic!^^
```

---

### Test Case 2

Rounds

```
(5,3) → Mishka wins
(6,2) → Mishka wins
```

Win counts

```
Mishka = 2
Chris = 0
```

Final Result

```
Mishka
```

## Complexity Analysis

### Time Complexity

**O(n)**
Each round is processed exactly once.

### Space Complexity

**O(1)**
Only constant extra variables are used.

## Solution Explanation

The solution uses two counters to track round victories for Mishka and Chris.
By comparing scores in each round and updating the counters accordingly, the final result is determined after all rounds are processed.

This approach is simple, efficient, and directly matches the problem requirements.

## Full Solution

### C++ Implementation

```cpp
#include <iostream>
using namespace std;

int main() {

    // Number of rounds
    int n;

    // Counters for Mishka's and Chris's wins
    int mishka = 0, chris = 0;

    // Read number of rounds
    cin >> n;

    // Process each round
    for (int i = 0; i < n; i++) {

        // Scores of Mishka and Chris for the round
        int a, b;
        cin >> a >> b;

        // Compare scores and update win counters
        if (a > b) {
            mishka++;
        }
        else if (a < b) {
            chris++;
        }
        // If a == b, no one gets a point
    }

    // Determine and print the final result
    if (mishka == chris) {
        cout << "Friendship is magic!^^";
    }
    else if (mishka > chris) {
        cout << "Mishka";
    }
    else {
        cout << "Chris";
    }

    return 0;
}
```

## Test Cases Analysis

| Rounds | Mishka Wins | Chris Wins | Output                 |
| ------ | ----------- | ---------- | ---------------------- |
| 3      | 1           | 1          | Friendship is magic!^^ |
| 2      | 2           | 0          | Mishka                 |
| 1      | 0           | 1          | Chris                  |
| 1      | 0           | 0          | Friendship is magic!^^ |

## Edge Cases to Consider

* All rounds end in a draw
* Only one round is played
* One player wins every round

## Common Test Cases

* Equal number of wins
* Clear winner
* Mixed wins and draws

## Common Mistakes to Avoid

* Counting draw rounds incorrectly
* Forgetting to initialize counters
* Printing incorrect output strings

## Interview Relevance

* Tests basic loop and conditional logic
* Evaluates counting-based decision making
* Common beginner-level comparison problem

## What This Problem Teaches

* Handling multiple test cases logically
* Using counters effectively
* Translating problem statements into clear conditions

## Key Takeaways

* Simple comparisons can solve multi-round problems
* Keep logic clean and readable
* Always handle tie cases explicitly

## Problem Difficulty Analysis

This is an **Easy-level** problem.
It focuses on basic iteration and comparison logic, making it ideal for beginners and interview warm-ups.
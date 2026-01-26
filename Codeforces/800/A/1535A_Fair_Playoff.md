# A. Fair Playoff

## Platform

Codeforces

## Problem Link

[A. Fair Playoff](https://codeforces.com/problemset/problem/1535/A)

## Problem Statement

You are given multiple test cases.
For each test case, four integers are provided, representing the strengths of four players.

The players are divided into two semifinals:

* Semifinal 1: Player 1 vs Player 2
* Semifinal 2: Player 3 vs Player 4

The winner of each semifinal is the player with the higher strength.

The playoff is considered **fair** if the **two strongest players overall** can meet in the final.

Your task is to determine whether the playoff setup is fair.

## Input Format

* The first line contains an integer `t`, the number of test cases.
* Each test case contains four integers `s1, s2, s3, s4` — the strengths of the players.

## Output Format

For each test case, print:

* `YES` if the playoff is fair
* `NO` otherwise

## Constraints

* `1 ≤ t ≤ 10^4`
* `1 ≤ s1, s2, s3, s4 ≤ 100`

## Examples

### Example 1

Input

```
3
1 4 2 3
5 3 6 4
1 2 3 4
```

Explanation

* Test case 1:

  * Semifinal winners: `4` and `3`
  * Two strongest overall: `4` and `3`
  * They meet in the final → fair
* Test case 2:

  * Semifinal winners: `5` and `6`
  * Two strongest overall: `6` and `5`
  * They meet in the final → fair
* Test case 3:

  * Semifinal winners: `2` and `4`
  * Two strongest overall: `4` and `3`
  * Player `3` is eliminated early → not fair

Output

```
YES
YES
NO
```

### Example 2

Input

```
1
10 1 2 3
```

Explanation

* Semifinal winners: `10` and `3`
* Two strongest overall: `10` and `3`
* They meet in the final → fair

Output

```
YES
```

## Approach

Comparison of semifinal winners and losers.

## Intuition

For the playoff to be fair:

* Each semifinal produces exactly one winner
* The **two strongest players overall** must both survive their semifinals

This condition is satisfied if **neither semifinal eliminates one of the two strongest players**.

Equivalently:

* The stronger loser among the two semifinals must not be stronger than the weaker winner

## Algorithm Steps

* Read the number of test cases `t`
* For each test case:

  * Read the four strengths into an array
  * Compute:

    * `w1` = stronger of the first semifinal
    * `w2` = stronger of the second semifinal
    * `l1` = weaker of the first semifinal
    * `l2` = weaker of the second semifinal
  * If `max(l1, l2) > min(w1, w2)`, print `NO`
  * Otherwise, print `YES`

## Visual Walkthrough

### Test Case 1

Input:

```
1 4 2 3
```

Semifinals:

```
(1 vs 4) → winner = 4
(2 vs 3) → winner = 3
```

Winners:

```
4, 3
```

Losers:

```
1, 2
```

Check:

```
max(1,2) = 2
min(4,3) = 3
2 ≤ 3 → fair
```

Result:

```
YES
```

---

### Test Case 2

Input:

```
1 2 3 4
```

Semifinals:

```
(1 vs 2) → winner = 2
(3 vs 4) → winner = 4
```

Losers:

```
1, 3
```

Check:

```
max(1,3) = 3
min(2,4) = 2
3 > 2 → unfair
```

Result:

```
NO
```

## Complexity Analysis

### Time Complexity

O(t)

Each test case uses a constant number of comparisons.

### Space Complexity

O(1)

Only a fixed-size array and a few variables are used.

## Solution Explanation

The solution ensures fairness by validating that the two strongest players are not eliminated in the semifinals.

By comparing the strongest loser against the weakest winner, the algorithm directly verifies whether the final can contain the top two players.

This method is both efficient and logically sound.

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

        // Strengths of the four players
        int s[4];
        cin >> s[0] >> s[1] >> s[2] >> s[3];

        // Winners of the two semifinals
        int w1 = max(s[0], s[1]);
        int w2 = max(s[2], s[3]);

        // Losers of the two semifinals
        int l1 = min(s[0], s[1]);
        int l2 = min(s[2], s[3]);

        // Check if the playoff is fair
        if (max(l1, l2) > min(w1, w2))
            cout << "NO\n";
        else
            cout << "YES\n";
    }

    return 0;
}
```

## Test Cases Analysis

| Strengths | Output | Reason                |
| --------- | ------ | --------------------- |
| 1 4 2 3   | YES    | Top two reach final   |
| 5 3 6 4   | YES    | Winners are strongest |
| 1 2 3 4   | NO     | Player 3 eliminated   |
| 10 1 2 3  | YES    | Strongest preserved   |

## Edge Cases to Consider

* Two strongest players in the same semifinal
* Equal strength values
* Minimum and maximum strength values

## Common Test Cases

* Increasing order strengths
* Decreasing order strengths
* Mixed strengths across semifinals

## Common Mistakes to Avoid

* Comparing only semifinal winners
* Ignoring the effect of losers
* Overcomplicating the logic

## Interview Relevance

* Tests logical reasoning
* Evaluates comparison-based decision making
* Common elimination tournament problem

## What This Problem Teaches

* Tournament simulation logic
* Importance of preserving optimal candidates
* Translating fairness conditions into code

## Key Takeaways

* Strongest participants must survive early rounds
* Simple comparisons can validate complex conditions
* Clear logic leads to concise solutions

## Problem Difficulty Analysis

This is an **Easy-level** problem.
It emphasizes logical comparisons and careful condition checking rather than complex algorithms.
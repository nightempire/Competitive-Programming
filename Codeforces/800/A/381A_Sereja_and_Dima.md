# A. Sereja and Dima

## Platform

Codeforces

## Problem Link

[A. Sereja and Dima](https://codeforces.com/problemset/problem/381/A)

## Problem Statement

Sereja and Dima are playing a game with a row of cards.
Each card has a number written on it.

The players take turns, starting with **Sereja**.
On each turn, a player chooses **either the leftmost or rightmost card**, takes it, and adds its value to their score.

Both players always play **optimally**, choosing the larger of the two available cards.

The game continues until no cards remain.

Determine the final scores of Sereja and Dima.

## Input Format

* The first line contains an integer `n`, the number of cards.
* The second line contains `n` integers representing the values on the cards.

## Output Format

Print two integers:

* Sereja’s final score
* Dima’s final score

## Constraints

* `1 ≤ n ≤ 1000`
* `1 ≤ card value ≤ 1000`

## Examples

### Example 1

Input

```
4
4 1 2 10
```

Explanation

* Sereja picks `10`
* Dima picks `4`
* Sereja picks `2`
* Dima picks `1`

Output

```
12 5
```

### Example 2

Input

```
3
1 2 3
```

Explanation

* Sereja picks `3`
* Dima picks `2`
* Sereja picks `1`

Output

```
4 2
```

### Example 3

Input

```
1
100
```

Explanation
Only one card, Sereja takes it.

Output

```
100 0
```

## Approach

**Two-Pointer Greedy Simulation**

## Intuition

Since both players always choose the maximum value available from either end, the game can be simulated directly.

By maintaining two pointers pointing to the leftmost and rightmost cards, we can decide which card is picked on each turn and alternate turns between the players.

## Algorithm Steps

* Read the number of cards
* Store card values in an array
* Initialize two pointers: left and right
* Initialize scores for Sereja and Dima
* Use a boolean flag to track turns
* While cards remain:

  * Pick the larger value between left and right
  * Add it to the current player’s score
  * Move the corresponding pointer
  * Switch turns
* Output both scores

## Visual Walkthrough

Cards:

```
[4, 1, 2, 10]
```

Step-by-step:

```
Turn 1 (Sereja): pick 10 → S = 10
Turn 2 (Dima):   pick 4  → D = 4
Turn 3 (Sereja): pick 2  → S = 12
Turn 4 (Dima):   pick 1  → D = 5
```

Final result:

```
Sereja = 12
Dima = 5
```

Another case:

```
[1, 2, 3]
Sereja → 3
Dima   → 2
Sereja → 1
```

## Complexity Analysis

### Time Complexity

O(n)

Each card is picked exactly once.

### Space Complexity

O(n)

An array is used to store card values.

## Solution Explanation

The solution simulates the game exactly as described.
By always choosing the larger value between the two ends and alternating turns, the optimal strategy is naturally enforced.
This greedy approach guarantees correct results due to the problem’s constraints.

## Full Solution

### C++ Implementation

```cpp
#include <iostream>
#include <algorithm>
using namespace std;

int main() {

    // Number of cards
    int n;
    cin >> n;

    // Array to store card values
    int nums[n];
    for (int i = 0; i < n; i++) {
        cin >> nums[i];
    }

    // Two pointers to track leftmost and rightmost cards
    int left = 0;
    int right = n - 1;

    // Scores of Sereja and Dima
    int sereja = 0;
    int dima = 0;

    // true  -> Sereja's turn
    // false -> Dima's turn
    bool turn = true;

    // Continue until all cards are taken
    while (left <= right) {

        int pick;

        // Choose the larger card from either end
        if (nums[left] > nums[right]) {
            pick = nums[left++];
        } else {
            pick = nums[right--];
        }

        // Add picked value to the current player's score
        if (turn) {
            sereja += pick;
        } else {
            dima += pick;
        }

        // Switch turn
        turn = !turn;
    }

    // Output final scores
    cout << sereja << " " << dima << '\n';

    return 0;
}
```

## Test Cases Analysis

| Cards    | Sereja Score | Dima Score |
| -------- | ------------ | ---------- |
| 4 1 2 10 | 12           | 5          |
| 1 2 3    | 4            | 2          |
| 100      | 100          | 0          |
| 5 5 5 5  | 10           | 10         |

## Edge Cases to Consider

* Only one card
* All cards have equal values
* Large `n` with alternating high/low values

## Common Test Cases

* Increasing order
* Decreasing order
* Symmetric values
* Single-element input

## Common Mistakes to Avoid

* Forgetting to alternate turns
* Incorrect pointer updates
* Using non-greedy selection

## Interview Relevance

* Tests greedy reasoning
* Demonstrates two-pointer technique
* Evaluates simulation skills

## What This Problem Teaches

* Effective use of two-pointer strategies
* Translating game rules into logic
* Greedy algorithms in practice

## Key Takeaways

* Always model the problem rules directly
* Two pointers simplify end-based selections
* Greedy simulation is often sufficient

## Problem Difficulty Analysis

This is an **Easy-level** problem.
It focuses on simulation and greedy decision-making, making it suitable for beginners and early interview rounds.
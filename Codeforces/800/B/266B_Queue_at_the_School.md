# B. Queue at the School

## Platform

Codeforces

## Problem Link

[B. Queue at the School](https://codeforces.com/problemset/problem/266/B)

## Problem Statement

There is a queue of students at a school.
Each student is represented by a character:

* `'B'` — a boy
* `'G'` — a girl

The queue evolves over time according to the following rule:

During each second, every boy who is **immediately in front of a girl** swaps positions with that girl.
All swaps in one second occur **simultaneously**.

Given the initial queue configuration and the number of seconds `t`, determine the final arrangement of the queue.

## Input Format

* The first line contains two integers `n` and `t`

  * `n` — number of students in the queue
  * `t` — number of seconds
* The second line contains a string `s` of length `n` consisting only of characters `'B'` and `'G'`

## Output Format

Print the final state of the queue after `t` seconds.

## Constraints

* `1 ≤ n ≤ 50`
* `1 ≤ t ≤ 50`
* `s[i] ∈ { 'B', 'G' }`

## Examples

### Example 1

Input

```
5 1
BGGBG
```

Explanation

After 1 second:

```
BGGBG → GBGGB
```

Output

```
GBGGB
```

### Example 2

Input

```
5 2
BGGBG
```

Explanation

Second-by-second evolution:

```
Second 1: BGGBG → GBGGB
Second 2: GBGGB → GGBGB
```

Output

```
GGBGB
```

## Approach

Simulation using iterative swaps with index skipping.

## Intuition

Each second represents a **simultaneous transformation** of the queue.

To simulate simultaneity using a loop:

* Traverse the queue from left to right
* When a `'B'` is followed by a `'G'`, swap them
* Skip the next index after a swap to avoid double movement in the same second

Repeating this process for `t` seconds yields the final queue state.

## Algorithm Steps

* Read integers `n` and `t`
* Read the string `s`
* Repeat the following process `t` times:

  * Traverse the string from index `1` to `n - 1`
  * If `s[i - 1]` is `'B'` and `s[i]` is `'G'`:

    * Swap the characters
    * Increment index by one extra step to prevent overlapping swaps
* Output the resulting string

## Visual Walkthrough

Initial queue:

```
B G G B G
```

After first second:

```
G B G G B
```

After second second:

```
G G B G B
```

Final queue:

```
GGBGB
```

## Complexity Analysis

### Time Complexity

**O(n × t)**
Each second requires a full scan of the queue.

### Space Complexity

**O(1)**
The queue is modified in place without additional memory usage.

## Solution Explanation

The solution simulates the queue’s behavior exactly as described.

The nested loop structure ensures:

* Each second is processed independently
* Each valid `'BG'` pair is swapped once per second
* Skipping indices after a swap prevents a student from moving multiple positions in the same second

This approach accurately models the simultaneous nature of the swaps while remaining efficient for the given constraints.

## Full Solution

### C++ Implementation

```cpp
#include <iostream>
using namespace std;

int main() {

    // Number of students and time duration
    int n, t;
    cin >> n >> t;

    // Initial queue representation
    string s;
    cin >> s;

    // Simulate each second
    while (t--) {

        // Traverse the queue
        for (int i = 1; i < n; i++) {

            // If a boy is immediately before a girl, swap them
            if (s[i - 1] == 'B' && s[i] == 'G') {

                char temp = s[i - 1];
                s[i - 1] = s[i];
                s[i] = temp;

                // Skip next index to avoid double swapping
                i++;
            }
        }
    }

    // Output final queue state
    cout << s << endl;

    return 0;
}
```

## Test Cases Analysis

| n | t | Initial Queue | Final Queue |
| - | - | ------------- | ----------- |
| 5 | 1 | BGGBG         | GBGGB       |
| 5 | 2 | BGGBG         | GGBGB       |
| 3 | 1 | BGG           | GBG         |
| 4 | 3 | BBBG          | GBBB        |

## Edge Cases to Consider

* Queue with all boys
* Queue with all girls
* Large `t` where no more swaps are possible

## Common Test Cases

* Alternating `'B'` and `'G'`
* All boys followed by all girls
* Single student queue

## Common Mistakes to Avoid

* Not skipping indices after a swap
* Attempting to swap in-place without handling simultaneity
* Incorrect loop boundaries

## Interview Relevance

* Tests simulation and string manipulation
* Reinforces careful loop control
* Common logical problem in coding interviews

## What This Problem Teaches

* Modeling simultaneous actions using sequential code
* Handling state changes safely
* Importance of index management in simulations

## Key Takeaways

* Simulations often require careful control flow
* Small constraints allow clean brute-force approaches
* Correctness depends on respecting problem rules exactly

## Problem Difficulty Analysis

This is an **Easy-to-Medium level** problem.

While conceptually simple, it requires careful handling of swaps to correctly simulate simultaneous movements.

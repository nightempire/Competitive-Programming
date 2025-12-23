# A. Magnets

## Platform

Codeforces

## Problem Link

[A. Magnets](https://codeforces.com/problemset/problem/344/A)

## Problem Statement

You are given `n` magnets placed in a row.

Each magnet is described by a string of two characters:

* `"01"`
* `"10"`

Adjacent magnets may attract or repel each other.
A **group** is formed when consecutive magnets have the same orientation.

Your task is to determine the **number of groups** formed by the magnets.

## Input Format

* The first line contains an integer `n`, the number of magnets
* The next `n` lines each contain a string representing a magnet’s orientation

## Output Format

Print a single integer representing the number of magnet groups.

## Constraints

* `1 ≤ n ≤ 100000`
* Each magnet is either `"01"` or `"10"`

## Examples

### Example 1

Input

```
6
10
10
10
01
10
10
```

Explanation

Grouping the magnets:

```
10 10 10 | 01 | 10 10
```

Total groups = `3`

Output

```
3
```

### Example 2

Input

```
4
01
01
10
10
```

Explanation

Grouping the magnets:

```
01 01 | 10 10
```

Total groups = `2`

Output

```
2
```

## Approach

Sequential comparison of adjacent magnets.

## Intuition

A new group starts whenever the orientation of the current magnet is **different** from the previous one.

By counting how many times the magnet orientation changes while reading the input, we can directly determine the total number of groups.

## Algorithm Steps

* Read integer `n`
* Read the first magnet and initialize group count to `1`
* For each remaining magnet:

  * Read current magnet
  * If it differs from the previous magnet:

    * Increment the group counter
    * Update the previous magnet
* Output the group count

## Visual Walkthrough

Input sequence:

```
10 10 01 01 10
```

Changes occur at:

```
10 → 01
01 → 10
```

Group formation:

```
10 10 | 01 01 | 10
```

Total groups = `3`

## Complexity Analysis

### Time Complexity

**O(n)**
Each magnet is processed once.

### Space Complexity

**O(1)**
Only two string variables are used.

## Solution Explanation

The solution reads magnets one by one and compares each magnet with the previous one.

If the orientation changes, it indicates the start of a new group.
The counter is incremented accordingly.

This method efficiently captures the grouping behavior without storing the entire sequence.

## Full Solution

### C++ Implementation

```cpp
#include <iostream>
using namespace std;

int main() {

    // Number of magnets
    int n;

    // Counter for magnet groups
    int count = 1;

    // Read number of magnets
    cin >> n;

    // Read the first magnet
    string prev, curr;
    cin >> prev;

    // Process remaining magnets
    for (int i = 1; i < n; i++) {

        cin >> curr;

        // If current magnet differs from previous,
        // a new group is formed
        if (prev != curr) {
            count++;
            prev = curr;
        }
    }

    // Output total number of groups
    cout << count << endl;

    return 0;
}
```

## Test Cases Analysis

| n | Magnet Sequence   | Groups |
| - | ----------------- | ------ |
| 1 | 10                | 1      |
| 3 | 10 10 10          | 1      |
| 4 | 10 01 10 01       | 4      |
| 6 | 10 10 10 01 10 10 | 3      |

## Edge Cases to Consider

* Only one magnet
* All magnets with same orientation
* Alternating magnet orientations

## Common Test Cases

* Large number of magnets with few changes
* Frequent orientation changes
* Minimum input size

## Common Mistakes to Avoid

* Forgetting to initialize group count to `1`
* Not reading the first magnet separately
* Incorrect comparison logic

## Interview Relevance

* Tests sequence analysis skills
* Evaluates handling of consecutive elements
* Common grouping/counting interview problem

## What This Problem Teaches

* Importance of comparing adjacent elements
* Efficient single-pass solutions
* Translating physical grouping into logical rules

## Key Takeaways

* Group counting problems often rely on detecting changes
* Sequential processing reduces memory usage
* Clear logic leads to simple and robust solutions

## Problem Difficulty Analysis

This is an **Easy-level** problem.

It focuses on basic iteration and comparison logic and is ideal for beginners and interview preparation.
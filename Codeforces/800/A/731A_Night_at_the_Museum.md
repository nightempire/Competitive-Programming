# A_Night_at_the_Museum

## Platform

Codeforces

## Problem Link

[A. Night at the Museum](https://codeforces.com/problemset/problem/731/A)

## Problem Statement

You are standing in a museum with a circular dial containing the lowercase English letters from `'a'` to `'z'` arranged in order.

Initially, the dial pointer is at letter `'a'`.

You are given a string `s`. To type each character of the string, you can rotate the dial either **clockwise** or **counterclockwise**. Each rotation by one letter costs **1 unit of time**.

Your task is to compute the **minimum total time** required to type the entire string.

## Input Format

* A single line containing a string `s`
* The string consists of lowercase English letters

## Output Format

* Print a single integer representing the minimum number of rotations needed

## Constraints

* `1 ≤ |s| ≤ 100`
* `s[i] ∈ {'a' ... 'z'}`

## Examples

### Example 1

Input

```
zeus
```

Explanation

Initial position: `'a'`

* `'a' → 'z'`
  Distance = 1 (counterclockwise)
* `'z' → 'e'`
  Distance = min(21, 5) = 5
* `'e' → 'u'`
  Distance = min(16, 10) = 10
* `'u' → 's'`
  Distance = min(2, 24) = 2

Total rotations = `1 + 5 + 10 + 2 = 18`

Output

```
18
```

---

### Example 2

Input

```
a
```

Explanation

The pointer starts at `'a'`, so no rotation is needed.

Output

```
0
```

---

### Example 3

Input

```
abc
```

Explanation

* `'a' → 'a'` = 0
* `'a' → 'b'` = 1
* `'b' → 'c'` = 1

Output

```
2
```

## Approach

**Greedy Distance Minimization on a Circular Alphabet**

## Intuition

The alphabet dial is circular, meaning:

* Moving forward from `'z'` leads back to `'a'`
* For any two letters, there are **two possible paths**

  * Clockwise
  * Counterclockwise

To minimize time, always choose the **shorter rotation path** between consecutive characters.

This greedy choice works because each character movement is independent and locally optimal.

## Algorithm Steps

* Read the input string `s`
* Initialize the pointer at `'a'`
* Compute the rotation cost to reach the first character
* For every subsequent character:

  * Calculate the absolute distance between current and previous character
  * Choose the minimum between:

    * Direct distance
    * Circular distance (`26 - direct distance`)
* Accumulate all rotation costs
* Output the total rotations

## Visual Walkthrough

### Case 1: `"c"`

```
'a' → 'c'
Direct distance = 2
Circular distance = 24
Choose 2
```

---

### Case 2: `"az"`

```
'a' → 'a' = 0
'a' → 'z'
Direct distance = 25
Circular distance = 1
Choose 1
```

---

### Case 3: `"za"`

```
'a' → 'z' = 1
'z' → 'a' = 1
Total = 2
```

## Complexity Analysis

### Time Complexity

**O(n)**

Each character in the string is processed exactly once.

### Space Complexity

**O(1)**

Only constant extra variables are used.

## Solution Explanation

The solution simulates the movement of a pointer on a circular alphabet dial.

For each transition between letters, it calculates:

* The direct distance
* The circular (wrap-around) distance

By always selecting the minimum of the two, the total number of rotations is minimized.

This greedy strategy is optimal due to the independence of each movement.

## Full Solution

### C++ Implementation

```cpp
#include <iostream>
using namespace std;

int main() {

    // Input string representing the sequence of letters to type
    string s;
    cin >> s;

    // Calculate rotations needed to reach the first character from 'a'
    int t = s[0] - 'a';
    int rotations = (t > 13) ? (26 - t) : t;

    // Calculate rotations for remaining characters
    for (int i = 1; i < s.length(); i++) {

        // Absolute difference between consecutive characters
        int t = abs(s[i] - s[i - 1]);

        // Add the minimum rotation distance (direct or circular)
        rotations += (t > 13) ? (26 - t) : t;
    }

    // Output the total minimum rotations
    cout << rotations << '\n';

    return 0;
}
```

## Test Cases Analysis

| Input String | Character Transitions | Total Rotations |
| ------------ | --------------------- | --------------- |
| `"a"`        | None                  | 0               |
| `"z"`        | a → z                 | 1               |
| `"abc"`      | a→b→c                 | 2               |
| `"za"`       | a→z→a                 | 2               |

## Edge Cases to Consider

* String of length 1
* Characters near `'a'` and `'z'`
* Maximum wrap-around distance
* Repeated same characters

## Common Test Cases

* Sequential letters
* Reverse order letters
* Random mixed letters

## Common Mistakes to Avoid

* Forgetting circular wrap-around logic
* Using only absolute difference
* Not handling the first character separately

## Interview Relevance

* Tests understanding of circular data structures
* Evaluates greedy decision-making
* Reinforces distance minimization concepts

## What This Problem Teaches

* Modeling circular structures
* Applying greedy strategies correctly
* Translating real-world movement into math

## Key Takeaways

* Circular distance often provides shorter paths
* Greedy local decisions can be globally optimal
* Always consider wrap-around in circular problems

## Problem Difficulty Analysis

This is an **Easy-level** problem.

The challenge lies in recognizing the circular nature of the alphabet and computing distances correctly, making it a common and effective interview warm-up problem.
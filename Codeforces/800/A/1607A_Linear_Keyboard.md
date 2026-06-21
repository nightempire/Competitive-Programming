# A. Linear Keyboard

## Platform

Codeforces

## Problem Link

[A. Linear Keyboard - Codeforces Problem 1607A](https://codeforces.com/problemset/problem/1607/A?utm_source=chatgpt.com)

## Problem Statement

A keyboard consists of the 26 lowercase English letters arranged in a specific linear order.

Typing a word requires moving a finger along this keyboard. The time required to move between two letters is equal to the absolute difference between their positions on the keyboard.

Given:

* A string representing the keyboard layout.
* A word to be typed.

Determine the total time required to type the word.

The finger starts on the first character of the word, so no movement cost is incurred before typing it.

## Input Format

* The first line contains an integer `t` — the number of test cases.
* For each test case:

  * A string of length `26` representing the keyboard layout.
  * A string `s` representing the word to be typed.

## Output Format

For each test case, print a single integer — the total typing time.

## Constraints

* `1 ≤ t ≤ 1000`
* Keyboard string contains all lowercase English letters exactly once.
* `1 ≤ |s| ≤ 50`
* `s` consists only of lowercase English letters.

## Examples

### Example 1

Input

```text
1
abcdefghijklmnopqrstuvwxyz
cba
```

Output

```text
3
```

### Explanation

Keyboard positions:

```text
a=1, b=2, c=3
```

Movements:

```text
c → b = 1
b → a = 1
```

Total time:

```text
1 + 1 = 2
```

Output:

```text
2
```

---

### Example 2

Input

```text
1
abcdefghijklmnopqrstuvwxyz
az
```

Output

```text
25
```

### Explanation

Positions:

```text
a = 1
z = 26
```

Movement:

```text
|26 - 1| = 25
```

Total time:

```text
25
```

---

### Example 3

Input

```text
1
qwertyuiopasdfghjklzxcvbnm
code
```

Output

```text
30
```

### Explanation

First determine the position of every character in the custom keyboard.

Then calculate:

```text
|pos(o)-pos(c)|
+ |pos(d)-pos(o)|
+ |pos(e)-pos(d)|
```

The sum of these distances gives the total typing time.

## Approach

### Algorithm Type

Position Mapping + Simulation

## Intuition

The keyboard layout is fixed for a test case.

To efficiently determine the movement cost between any two characters:

* Store the position of every character in an array.
* For each consecutive pair of characters in the word:

  * Find their keyboard positions.
  * Add the absolute difference to the answer.

This avoids repeatedly searching the keyboard string.

## Algorithm Steps

* Read the number of test cases `t`.
* For each test case:

  * Read the keyboard layout.
  * Read the word `s`.
  * Create an array of size 26.
  * Store the position of each letter in the keyboard.
  * Initialize `time = 0`.
  * Traverse the word from the second character onward:

    * Compute the distance between current and previous characters.
    * Add it to `time`.
  * Print `time`.

## Visual Walkthrough

### Test Case 1

Keyboard:

```text
abcdefghijklmnopqrstuvwxyz
```

Word:

```text
cba
```

Positions:

```text
c = 3
b = 2
a = 1
```

Movement:

```text
c → b = |3 - 2| = 1
b → a = |2 - 1| = 1
```

Total:

```text
1 + 1 = 2
```

Output:

```text
2
```

---

### Test Case 2

Keyboard:

```text
abcdefghijklmnopqrstuvwxyz
```

Word:

```text
az
```

Movement:

```text
a → z = |1 - 26| = 25
```

Output:

```text
25
```

---

### Test Case 3

Keyboard:

```text
abcdefghijklmnopqrstuvwxyz
```

Word:

```text
abca
```

Movements:

```text
a → b = 1
b → c = 1
c → a = 2
```

Total:

```text
1 + 1 + 2 = 4
```

Output:

```text
4
```

## Complexity Analysis

### Time Complexity

**O(26 + |s|)**

For each test case:

* Building the position map takes `O(26)`.
* Traversing the word takes `O(|s|)`.

Therefore:

```text
O(26 + |s|)
```

Since `26` is constant, it is effectively:

```text
O(|s|)
```

### Space Complexity

**O(26)**

The position array stores one position for each lowercase letter.

```text
Position Array Size = 26
```

Therefore:

```text
O(1)
```

constant extra space.

## Solution Explanation

The solution first maps every character of the keyboard layout to its position.

For example:

```text
keyboard = "abcdefghijklmnopqrstuvwxyz"
```

creates:

```text
a → 1
b → 2
c → 3
...
z → 26
```

Then, for every adjacent pair of characters in the word:

```text
s[i-1], s[i]
```

the movement cost is:

```text
abs(position[s[i]] - position[s[i-1]])
```

Adding all these distances produces the total typing time.

This method is efficient because each character position lookup takes constant time.

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

        // Keyboard layout and target word
        string keyboard, s;
        cin >> keyboard >> s;

        // Stores position of every character
        int f[26] = {0};

        // Total typing time
        int time = 0;

        // Length of the word
        int n = s.size();

        // Build character-to-position mapping
        for(int i = 0; i < 26; i++) {
            f[keyboard[i] - 'a'] = i + 1;
        }

        // Calculate movement cost
        for(int i = 1; i < n; i++) {

            // Add distance between consecutive characters
            time += abs(
                f[s[i] - 'a']
                - f[s[i - 1] - 'a']
            );
        }

        // Print total typing time
        cout << time << '\n';
    }

    return 0;
}
```

## Test Cases Analysis

| Keyboard Layout            | Word | Movement Calculation | Output            |
| -------------------------- | ---- | -------------------- | ----------------- |
| abcdefghijklmnopqrstuvwxyz | cba  | 1 + 1                | 2                 |
| abcdefghijklmnopqrstuvwxyz | az   | 25                   | 25                |
| abcdefghijklmnopqrstuvwxyz | abca | 1 + 1 + 2            | 4                 |
| abcdefghijklmnopqrstuvwxyz | a    | 0                    | 0                 |
| qwertyuiopasdfghjklzxcvbnm | code | Custom positions     | Depends on layout |

## Edge Cases to Consider

* Word length is `1`.
* Consecutive characters are identical.
* Movement between the first and last keyboard positions.
* Completely custom keyboard layouts.
* Repeated occurrences of the same character.

## Common Test Cases

### Single Character Word

```text
Input:
1
abcdefghijklmnopqrstuvwxyz
a

Output:
0
```

---

### Maximum Distance

```text
Input:
1
abcdefghijklmnopqrstuvwxyz
az

Output:
25
```

---

### Repeated Characters

```text
Input:
1
abcdefghijklmnopqrstuvwxyz
aaaa

Output:
0
```

---

### Mixed Movement

```text
Input:
1
abcdefghijklmnopqrstuvwxyz
abca

Output:
4
```

## Common Mistakes to Avoid

* Searching the keyboard string for every character instead of precomputing positions.
* Forgetting that the first character requires no movement.
* Using character indices directly without mapping them to keyboard positions.

## Interview Relevance

* Demonstrates preprocessing for fast lookups.
* Tests array-based character mapping techniques.
* Reinforces simulation and distance-calculation problems.

## What This Problem Teaches

* Building efficient lookup tables.
* Converting characters into indexed positions.
* Using preprocessing to reduce repeated work.

## Key Takeaways

* Precomputing positions enables constant-time character lookups.
* Consecutive-character processing is a common pattern in string problems.
* Small preprocessing steps can significantly simplify implementation.

## Problem Difficulty Analysis

This is an **Easy** implementation problem.

The main observation is that character positions should be precomputed once. After that, the solution becomes a straightforward traversal of the word while summing distances between consecutive characters. No advanced algorithms or data structures are required.
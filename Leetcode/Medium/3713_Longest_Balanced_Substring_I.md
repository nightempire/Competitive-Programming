# 3713. Longest Balanced Substring I

## Platform

LeetCode

## Problem Link

[3713. Longest Balanced Substring I](https://leetcode.com/problems/longest-balanced-substring-i/)

## Problem Statement

You are given a string `s` consisting of lowercase English letters.

A substring is called **balanced** if:

* All characters that appear in the substring have the **same frequency**.

Your task is to return the **length of the longest balanced substring**.

If no larger balanced substring exists, return `1`.

## Input Format

* A single string `s`
* `s` consists only of lowercase English letters

## Output Format

* Return an integer representing the maximum length of a balanced substring

## Constraints

* `1 ≤ s.length ≤ 100`
* `s[i] ∈ {'a' ... 'z'}`

## Examples

### Example 1

Input

```
"abab"
```

Explanation

Substring `"abab"`:

```
'a' → 2 times
'b' → 2 times
```

All characters appear with equal frequency.

Output

```
4
```

---

### Example 2

Input

```
"aaabb"
```

Explanation

Longest balanced substring is `"aabb"`:

```
'a' → 2
'b' → 2
```

Output

```
4
```

---

### Example 3

Input

```
"abc"
```

Explanation

Each character appears once.

Entire string is balanced.

Output

```
3
```

---

### Example 4

Input

```
"a"
```

Explanation

Single character substrings are always balanced.

Output

```
1
```

## Approach

**Frequency Sliding Window with Backward Iteration**

## Intuition

A substring is balanced if:

* All characters present in it have identical frequency.

The solution strategy:

* Maintain global frequency of characters.
* Fix a potential right boundary from the end of the string.
* Use a sliding window (`left`, `right`) to check substrings.
* Track frequency counts dynamically.
* If all non-zero frequencies match, return the substring length immediately.
* Continue shrinking and adjusting the window while updating frequency.

Since we iterate from larger substrings toward smaller ones, the first valid balanced substring found is the maximum.

## Algorithm Steps

* Compute total frequency of characters in the string.
* Iterate `i` from `n-1` to `0`:

  * Initialize `left = 0`, `right = i`
  * Copy current global frequency into `currFreq`
  * While `right < n`:

    * Let `x = frequency of character at left`
    * Check if all non-zero frequencies equal `x`
    * If yes, return substring length
    * Otherwise:

      * Decrease frequency of character at `left`
      * Move `left` forward
      * Increase `right` if possible
  * Reduce global frequency for character at index `i`
* If no longer balanced substring found, return `1`

## Visual Walkthrough

### Case 1: `"abab"`

Initial frequency:

```
a = 2
b = 2
```

Check full string:

```
All frequencies equal → balanced
Length = 4
```

---

### Case 2: `"aaabb"`

Initial frequency:

```
a = 3
b = 2
```

Full string → not balanced

Shrink window:

Check `"aabb"`:

```
a = 2
b = 2
Balanced → length = 4
```

---

### Case 3: `"abc"`

```
a = 1
b = 1
c = 1
Balanced → length = 3
```

## Complexity Analysis

### Time Complexity

Worst case: **O(n² × 26)**

* Outer loop runs up to `n`
* Inner sliding window runs up to `n`
* Frequency comparison checks up to 26 characters

Since `n ≤ 100`, this is acceptable.

### Space Complexity

**O(26)**

Fixed-size frequency arrays are used.

## Solution Explanation

The solution maintains two frequency arrays:

* `freq` → overall character counts
* `currFreq` → sliding window counts

For each candidate window:

* It verifies whether all present characters have identical frequency.
* As soon as such a substring is found (starting from larger windows), its length is returned.

This ensures correctness while respecting problem constraints.

## Full Solution

### C++ Implementation

```cpp
class Solution {
public:
    int longestBalanced(string s) {

        int n = s.length();

        // Global frequency array
        int freq[26] = {0};

        for (char ch : s)
            freq[ch - 'a']++;

        // Iterate potential right boundary backward
        for (int i = n - 1; i >= 0; i--) {

            int left = 0, right = i;

            // Copy global frequency to current window frequency
            int currFreq[26];
            for (int j = 0; j < 26; j++)
                currFreq[j] = freq[j];

            while (right < n) {

                bool flag = false;

                // Reference frequency
                int x = currFreq[s[left] - 'a'];

                // Check if all non-zero frequencies match x
                for (int y : currFreq) {
                    if (y > 0 && y != x) {
                        flag = true;
                        break;
                    }
                }

                // If balanced substring found
                if (!flag)
                    return right - left + 1;

                // Shrink window from left
                currFreq[s[left++] - 'a']--;

                if (right == n - 1)
                    break;

                // Expand window to the right
                currFreq[s[++right] - 'a']++;
            }

            // Reduce global frequency
            freq[s[i] - 'a']--;
        }

        return 1;
    }
};
```

## Test Cases Analysis

| Input     | Balanced Substring | Output |
| --------- | ------------------ | ------ |
| `"abab"`  | `"abab"`           | 4      |
| `"aaabb"` | `"aabb"`           | 4      |
| `"abc"`   | `"abc"`            | 3      |
| `"a"`     | `"a"`              | 1      |

## Edge Cases to Consider

* Single-character string
* All identical characters
* All distinct characters
* Mixed frequencies

## Common Test Cases

* Equal distribution of characters
* One character dominating frequency
* Multiple possible balanced substrings

## Common Mistakes to Avoid

* Checking total count instead of equal frequency
* Not ignoring zero frequencies
* Incorrect window shrinking logic

## Interview Relevance

* Tests sliding window techniques
* Evaluates frequency tracking
* Reinforces substring validation logic

## What This Problem Teaches

* Frequency-based substring analysis
* Combining sliding window with validation checks
* Efficient handling of character counts

## Key Takeaways

* Balanced substrings require equal frequency among present characters
* Fixed-size arrays are efficient for alphabet problems
* Early return ensures longest substring is captured first

## Problem Difficulty Analysis

This is a **Medium-level** problem.

The challenge lies in correctly managing sliding windows and validating equal frequency conditions efficiently.
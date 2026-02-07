# Minimum Deletions to Make String Balanced

## Platform

LeetCode

## Problem Link

[1653. Minimum Deletions to Make String Balanced](https://leetcode.com/problems/minimum-deletions-to-make-string-balanced/)

## Problem Statement

You are given a string `s` consisting only of the characters `'a'` and `'b'`.

A string is considered **balanced** if **there is no pair of indices `(i, j)` such that `i < j`, `s[i] = 'b'`, and `s[j] = 'a'`**.

In other words, all `'a'` characters must appear **before** any `'b'` characters.

Your task is to determine the **minimum number of deletions** required to make the string balanced.

## Input Format

* A single string `s`
* `s` consists only of lowercase characters `'a'` and `'b'`

## Output Format

* Return an integer representing the **minimum number of deletions** needed to make the string balanced

## Constraints

* `1 ≤ s.length ≤ 10^5`
* `s[i] ∈ {'a', 'b'}`

## Examples

### Example 1

Input

```
"aababbab"
```

Explanation

The invalid patterns are `"ba"` pairs.
Deleting one `'b'` before an `'a'` repeatedly resolves violations.

Output

```
2
```

---

### Example 2

Input

```
"bbaaaa"
```

Explanation

The `'b'` characters appear before `'a'`, violating balance.
Deleting both `'b'` characters fixes the order.

Output

```
2
```

---

### Example 3

Input

```
"aaaa"
```

Explanation

No `'b'` appears before `'a'`.
The string is already balanced.

Output

```
0
```

## Approach

**Greedy Algorithm using Stack Simulation**

## Intuition

A violation occurs **only** when a `'b'` appears **before** an `'a'`.

Each `"ba"` pattern means:

* Either delete the earlier `'b'`
* Or delete the later `'a'`

The greedy idea is:

* Whenever an `'a'` appears after a `'b'`, delete the `'b'` immediately
* This minimizes future violations

A stack helps track previously seen characters and detect violations efficiently.

## Algorithm Steps

* Initialize an empty stack
* Initialize a counter `count = 0`
* Traverse the string character by character
* For each character:

  * If the stack is **not empty**, and:

    * Current character is `'a'`
    * Stack top is `'b'`
  * Then:

    * Pop `'b'` from the stack
    * Increment deletion counter
  * Otherwise:

    * Push current character onto the stack
* Return the deletion counter

## Visual Walkthrough

### Case 1: `"ba"`

```
Stack: []
Read 'b' → push → [b]
Read 'a' → conflict ("ba")
Pop 'b', delete it
Count = 1
```

Balanced result: `"a"`

---

### Case 2: `"bba"`

```
Read 'b' → [b]
Read 'b' → [b, b]
Read 'a' → conflict
Pop 'b', Count = 1
```

Remaining stack: `[b]`
Final balanced string after deletions: `"ba"` → further handled during traversal

---

### Case 3: `"aabb"`

```
Read all characters
No "ba" pattern found
Count = 0
```

## Complexity Analysis

### Time Complexity

**O(n)**

Each character is pushed and popped **at most once** from the stack.

### Space Complexity

**O(n)**

In the worst case, all characters are stored in the stack.

## Solution Explanation

The solution simulates the process of removing invalid `"ba"` pairs greedily.

Whenever an `'a'` is found after a `'b'`, the earlier `'b'` is deleted immediately.
This ensures:

* Minimum deletions
* No unnecessary removals
* Linear time processing

The stack acts as a history of valid characters while efficiently detecting violations.

## Full Solution

### C++ Implementation

```cpp
class Solution {
public:
    int minimumDeletions(string s) {

        // Stack to track previously processed characters
        stack<char> stk;

        // Counter to store the number of deletions performed
        int count = 0;

        // Traverse each character in the string
        for (char ch : s) {

            // If a violation "ba" is found
            if (!stk.empty() && ch == 'a' && stk.top() == 'b') {

                // Remove the 'b' to fix the violation
                stk.pop();

                // Increment deletion count
                count++;

            } else {
                // Otherwise, push the character into the stack
                stk.push(ch);
            }
        }

        // Return the minimum number of deletions
        return count;
    }
};
```

## Test Cases Analysis

| Input String | Stack Operations Summary      | Deletions |
| ------------ | ----------------------------- | --------- |
| `"aababb"`   | Two `"ba"` conflicts resolved | 2         |
| `"bbbb"`     | No conflicts                  | 0         |
| `"bbaa"`     | Two `'b'` removed             | 2         |
| `"abab"`     | One conflict                  | 1         |

## Edge Cases to Consider

* String containing only `'a'`
* String containing only `'b'`
* Alternating patterns like `"abababab"`
* Minimum length string (`length = 1`)

## Common Test Cases

* Already balanced strings
* Strings with leading `'b'`s and trailing `'a'`s
* Large input sizes to test performance

## Common Mistakes to Avoid

* Counting `"ab"` instead of `"ba"`
* Forgetting to check if the stack is empty
* Deleting `'a'` instead of the conflicting `'b'`

## Interview Relevance

* Tests greedy decision-making
* Evaluates stack usage and string traversal
* Common pattern-removal problem in interviews

## What This Problem Teaches

* How greedy strategies simplify constraint problems
* Stack-based pattern detection
* Efficient handling of ordered character constraints

## Key Takeaways

* Only `"ba"` patterns violate balance
* Greedy removal ensures minimum deletions
* Stack simulation provides clean and efficient logic

## Problem Difficulty Analysis

This is a **Medium-level** problem.

While the logic is simple, identifying the correct greedy choice and implementing it efficiently requires solid understanding of stacks and pattern-based reasoning.
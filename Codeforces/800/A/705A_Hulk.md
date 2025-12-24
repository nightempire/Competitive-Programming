# A_Hulk

## Platform

Codeforces

## Problem Link

[A. Hulk](https://codeforces.com/problemset/problem/705/A)

## Problem Statement

Dr. Bruce Banner hates programming, but he loves algorithms.
However, his feelings are inconsistent and follow a specific pattern.

Given an integer `n`, representing the number of emotions, you must generate a sentence describing Hulk’s feelings using the following rules:

* The sentence starts with **"I hate"**
* Feelings alternate between **"I hate"** and **"I love"**
* Each feeling is connected using the word **"that"**
* The sentence must always end with **"it"**

Your task is to print the complete sentence following this pattern.

## Input Format

* A single integer `n`
  The number of emotions.

## Output Format

* Print a single sentence describing Hulk’s feelings.

## Constraints

* `1 ≤ n ≤ 100`

## Examples

### Example 1

Input

```
1
```

Explanation

Only one emotion exists, so the sentence contains just the starting phrase.

Output

```
I hate it
```

---

### Example 2

Input

```
2
```

Explanation

The emotions alternate:

* First → hate
* Second → love

Output

```
I hate that I love it
```

---

### Example 3

Input

```
3
```

Explanation

The emotions alternate again:

* hate → love → hate

Output

```
I hate that I love that I hate it
```

## Approach

**Pattern-based string construction using iteration**

## Intuition

The problem follows a **fixed alternating pattern**:

* Odd positions → `"I hate"`
* Even positions → `"I love"`

By building the sentence step by step and appending each phrase with `"that"`, the final result can be constructed efficiently using a loop.

## Algorithm Steps

* Read the integer `n`
* Initialize the result string with `"I hate"`
* Loop from `2` to `n`:

  * If the index is odd, append `"that I hate"`
  * If the index is even, append `"that I love"`
* Append `" it"` at the end
* Output the final sentence

## Visual Walkthrough

### Case 1

Input

```
n = 1
```

Construction

```
I hate
```

Final Output

```
I hate it
```

---

### Case 2

Input

```
n = 2
```

Construction

```
I hate
→ that I love
```

Final Output

```
I hate that I love it
```

---

### Case 3

Input

```
n = 4
```

Construction

```
I hate
→ that I love
→ that I hate
→ that I love
```

Final Output

```
I hate that I love that I hate that I love it
```

## Complexity Analysis

### Time Complexity

**O(n)**

Each emotion is processed exactly once, and a fixed amount of string concatenation is performed per iteration.

### Space Complexity

**O(n)**

The resulting string grows linearly with the number of emotions.

## Solution Explanation

The solution constructs the sentence incrementally:

* It starts with `"I hate"` since the first emotion is always hate
* Each subsequent emotion is appended using `"that"`
* The parity of the loop index determines whether to append `"I hate"` or `"I love"`
* Finally, `" it"` is added to complete the sentence

This approach keeps the logic simple and mirrors the problem description exactly.

## Full Solution

### C++ Implementation

```cpp
#include <iostream>
using namespace std;

int main() {

    // Number of emotions
    int n;
    cin >> n;

    // Base phrases
    string res;
    string hate = "I hate";
    string love = "I love";

    // The sentence always starts with "I hate"
    res = hate;

    // Build the rest of the sentence
    for (int i = 2; i <= n; i++) {

        // Odd index → hate
        if (i & 1) {
            res += " that " + hate;
        }
        // Even index → love
        else {
            res += " that " + love;
        }
    }

    // End the sentence with " it"
    cout << res + " it" << endl;

    return 0;
}
```

## Test Cases Analysis

| Input `n` | Expected Output                               |
| --------- | --------------------------------------------- |
| 1         | I hate it                                     |
| 2         | I hate that I love it                         |
| 3         | I hate that I love that I hate it             |
| 4         | I hate that I love that I hate that I love it |

## Edge Cases to Consider

* Minimum value of `n` (`n = 1`)
* Larger values of `n` with repeated alternation
* Correct placement of `"that"` and `"it"`

## Common Test Cases

* Single emotion
* Even number of emotions
* Odd number of emotions

## Common Mistakes to Avoid

* Forgetting to append `" it"` at the end
* Incorrect alternation logic
* Adding extra `"that"` before `"it"`

## Interview Relevance

* Tests string manipulation skills
* Evaluates understanding of patterns and loops
* Common beginner-level logic problem

## What This Problem Teaches

* Pattern recognition
* Conditional logic based on index parity
* Clean construction of structured output strings

## Key Takeaways

* Always identify repeating patterns before coding
* Parity checks simplify alternating logic
* String construction problems reward clarity over complexity

## Problem Difficulty Analysis

This is an **Easy-level** problem.

It focuses on pattern-based logic and string concatenation, making it ideal for beginners and early competitive programming practice.
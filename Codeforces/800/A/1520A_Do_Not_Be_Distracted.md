# A. Do Not Be Distracted!

## Platform

Codeforces

## Problem Link

[A. Do Not Be Distracted!](https://codeforces.com/problemset/problem/1520/A)

## Problem Statement

You are given multiple test cases.
For each test case, you are given:

* An integer `n`, the length of a string.
* A string `s` consisting of uppercase English letters.

Each character represents a task.
Once you stop working on a particular task, **you must never return to it again**.

Your task is to determine whether the string follows this rule.

* Print `YES` if the rule is followed.
* Print `NO` otherwise.

## Input Format

* The first line contains an integer `t`, the number of test cases.
* For each test case:

  * An integer `n`, the length of the string.
  * A string `s` of length `n` consisting of uppercase English letters.

## Output Format

For each test case, print `YES` if the task sequence is valid.
Otherwise, print `NO`.

## Constraints

* `1 ≤ t ≤ 1000`
* `1 ≤ n ≤ 50`
* `s` contains only uppercase English letters (`A` to `Z`)

## Examples

### Example 1

Input

```
3
3
ABA
4
AABB
5
ABBBA
```

Explanation

* Test case 1: Task `A` appears again after switching to `B` → invalid
* Test case 2: Each task is continuous → valid
* Test case 3: Task `A` appears only once, `B` is continuous → valid

Output

```
NO
YES
YES
```

### Example 2

Input

```
1
6
ABCABC
```

Explanation

Tasks repeat after interruption, violating the rule.

Output

```
NO
```

## Approach

Character tracking using a boolean frequency array.

## Intuition

A task is allowed to appear **only in one continuous block**.
If a character reappears after a different character occurs in between, the rule is violated.

To detect this:

* Track which tasks have already appeared.
* Compare each character with the previous one.
* If a task reappears after interruption, the sequence is invalid.

## Algorithm Steps

* Read the number of test cases `t`.
* For each test case:

  * Read `n` and string `s`.
  * Initialize a boolean array of size 26 to track visited characters.
  * Mark the first character as visited.
  * Traverse the string from index `1` to `n - 1`:

    * If the current character differs from the previous one:

      * If it was already visited, mark the sequence invalid.
      * Otherwise, mark it as visited.
  * Print `NO` if invalid, else print `YES`.

## Visual Walkthrough

### Test Case 1

Input:

```
ABA
```

Progression:

```
A → B → A
```

Observation:

```
Task A reappears after interruption → invalid
```

Result:

```
NO
```

---

### Test Case 2

Input:

```
AABB
```

Progression:

```
A → A → B → B
```

Observation:

```
Each task appears in one continuous block
```

Result:

```
YES
```

---

### Test Case 3

Input:

```
ABBBA
```

Progression:

```
A → B → B → B → A
```

Observation:

```
Task A reappears after interruption → invalid
```

Result:

```
NO
```

## Complexity Analysis

### Time Complexity

O(n) per test case

Each character in the string is processed exactly once.

### Space Complexity

O(1)

A fixed-size boolean array of length 26 is used, independent of input size.

## Solution Explanation

The solution ensures that once a task is completed and another task begins, the completed task never appears again.
By tracking previously visited tasks and comparing consecutive characters, violations are detected efficiently.

This approach is optimal and directly enforces the problem constraint.

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

        // Length of the string
        int n;
        cin >> n;

        // Task sequence string
        string s;
        cin >> s;

        // Boolean array to track whether a task has appeared before
        bool visited[26] = {false};

        // Flag to indicate invalid task sequence
        bool invalid = false;

        // Mark the first task as visited
        visited[s[0] - 'A'] = true;

        // Traverse the string from the second character
        for (int i = 1; i < n; i++) {

            // If current task differs from the previous task
            if (s[i] != s[i - 1]) {

                // If the task was already visited, it is invalid
                if (visited[s[i] - 'A']) {
                    invalid = true;
                    break;
                }

                // Mark the new task as visited
                visited[s[i] - 'A'] = true;
            }
        }

        // Output result for the current test case
        cout << (invalid ? "NO\n" : "YES\n");
    }

    return 0;
}
```

## Test Cases Analysis

| Test Case | Input String | Output | Reason                 |
| --------- | ------------ | ------ | ---------------------- |
| 1         | `A`          | YES    | Single task            |
| 2         | `AAABBB`     | YES    | Continuous blocks      |
| 3         | `ABA`        | NO     | Task repeats           |
| 4         | `ABC`        | YES    | No repetition          |
| 5         | `ABCA`       | NO     | Interrupted repetition |

## Edge Cases to Consider

* String of length `1`
* All characters same
* Immediate repetition after a single different character

## Common Test Cases

* Strings with alternating characters
* Strings with long continuous blocks
* Strings where a character reappears at the end

## Common Mistakes to Avoid

* Not tracking previously visited tasks
* Only checking adjacent characters
* Forgetting to reset tracking for each test case

## Interview Relevance

* Tests string traversal logic
* Evaluates state tracking techniques
* Common problem for validating constraints

## What This Problem Teaches

* Importance of tracking state changes
* Handling character-based constraints
* Efficient validation using constant space

## Key Takeaways

* Continuous grouping matters in sequence problems
* Boolean tracking can simplify validation
* Clean iteration avoids unnecessary complexity

## Problem Difficulty Analysis

This is an **Easy-level** problem.
It emphasizes careful observation and disciplined state tracking rather than advanced algorithms.
# A. Codeforces Checking

## Platform

Codeforces

## Problem Link

[A. Codeforces Checking](https://codeforces.com/problemset/problem/1791/A)

## Problem Statement

You are given a character for each test case.

Your task is to determine whether the given character appears in the string:

```
"codeforces"
```

If the character exists in the string, print `"YES"`.
Otherwise, print `"NO"`.

## Input Format

* The first line contains an integer `t`, the number of test cases.
* Each test case contains a single character `ch`.

## Output Format

For each test case, print `"YES"` or `"NO"` on a new line.

## Constraints

* `1 ≤ t ≤ 1000`
* `ch` is a lowercase English letter

## Examples

### Example 1

Input

```
5
c
a
o
z
s
```

Explanation

* `c` appears in `"codeforces"` → `YES`
* `a` does not appear → `NO`
* `o` appears → `YES`
* `z` does not appear → `NO`
* `s` appears → `YES`

Output

```
YES
NO
YES
NO
YES
```

### Example 2

Input

```
3
d
e
f
```

Output

```
YES
YES
YES
```

## Approach

**Direct Character Matching Using Switch Statement**

## Intuition

The string `"codeforces"` contains a **fixed and small set of unique characters**:

```
{ c, o, d, e, f, r, s }
```

Since the set is constant, the fastest and simplest approach is to directly check whether the input character matches any of these characters.

Using a `switch` statement allows:

* Clear intent
* Constant-time checking
* No extra memory usage

## Algorithm Steps

* Read the number of test cases
* For each test case:

  * Read character `ch`
  * Use a `switch` statement to check if `ch` matches any character in `"codeforces"`
  * Print `"YES"` if matched
  * Otherwise, print `"NO"`

## Visual Walkthrough

Input character:

```
ch = 'r'
```

Switch cases checked:

```
'c', 'o', 'd', 'e', 'f', 'r', 's'
```

Match found → Output:

```
YES
```

Another case:

```
ch = 'x'
```

No match → Output:

```
NO
```

## Complexity Analysis

### Time Complexity

O(t)

Each test case is handled in constant time.

### Space Complexity

O(1)

No additional data structures are used.

## Solution Explanation

The solution avoids unnecessary string traversal or data structures.
Because the valid characters are known in advance, a `switch` statement provides a clean and efficient solution.

Each case corresponds to one valid character from `"codeforces"`.

## Full Solution

### C++ Implementation

```cpp
#include <iostream>
using namespace std;

int main() {

    // Number of test cases
    int t;
    cin >> t;

    // Process each test case
    while (t--) {

        // Read the character
        char ch;
        cin >> ch;

        // Check if the character exists in "codeforces"
        switch (ch) {

            case 'c':
            case 'o':
            case 'd':
            case 'e':
            case 'f':
            case 'r':
            case 's':
                cout << "YES\n";
                break;

            default:
                cout << "NO\n";
        }
    }

    return 0;
}
```

## Test Cases Analysis

| Character | In "codeforces" | Output |
| --------: | --------------- | ------ |
|         c | Yes             | YES    |
|         a | No              | NO     |
|         o | Yes             | YES    |
|         z | No              | NO     |
|         s | Yes             | YES    |

## Edge Cases to Consider

* Repeated characters across test cases
* Characters not present in the string
* Minimum and maximum number of test cases

## Common Test Cases

* Characters from `"codeforces"`
* Random lowercase letters

## Common Mistakes to Avoid

* Checking uppercase characters unnecessarily
* Forgetting `break` statements in `switch`
* Overcomplicating with strings or sets

## Interview Relevance

* Tests basic conditional logic
* Demonstrates understanding of constant sets
* Encourages clean and readable code

## What This Problem Teaches

* Using control flow effectively
* Choosing the simplest valid approach
* Avoiding unnecessary data structures

## Key Takeaways

* Fixed sets can be handled with direct comparisons
* `switch` statements are ideal for small known domains
* Simplicity improves clarity and performance

## Problem Difficulty Analysis

This is an **Easy-level** problem.
It focuses on straightforward character checking and basic control flow, making it ideal for beginners and quick practice.
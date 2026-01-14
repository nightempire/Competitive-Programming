# A_Black_Square

## Platform

Codeforces

## Problem Link

[A. Black Square](https://codeforces.com/problemset/problem/431/A)

## Problem Statement

You are given calorie values for stepping on four different black squares in a game.

Each square corresponds to a digit:

* `'1'` → first square
* `'2'` → second square
* `'3'` → third square
* `'4'` → fourth square

You are also given a string consisting of digits from `'1'` to `'4'`.
Each digit represents stepping on the corresponding square **once**.

Your task is to calculate the **total calories burned** after stepping on all the squares represented by the string.

## Input Format

* The first line contains four integers, representing the calorie values of squares `1` to `4`.
* The second line contains a string `s`, consisting only of characters `'1'`, `'2'`, `'3'`, and `'4'`.

## Output Format

Print a single integer representing the total calories burned.

## Constraints

* `1 ≤ calorie value ≤ 100`
* `1 ≤ |s| ≤ 1000`
* `s[i] ∈ { '1', '2', '3', '4' }`

## Examples

### Example 1

Input

```
1 2 3 4
1234
```

Explanation

* Step on square `1` → 1 calorie
* Step on square `2` → 2 calories
* Step on square `3` → 3 calories
* Step on square `4` → 4 calories

Total

```
1 + 2 + 3 + 4 = 10
```

Output

```
10
```

### Example 2

Input

```
4 3 2 1
12121
```

Explanation

```
4 + 3 + 4 + 3 + 4 = 18
```

Output

```
18
```

## Approach (Algorithm Name / Type)

**Direct Mapping and Accumulation**

## Intuition

Each character in the string directly maps to one of the four calorie values.

By converting the character digit (`'1'` to `'4'`) into an index and adding the corresponding calorie value, we can compute the total efficiently in a single traversal.

## Algorithm Steps

* Read the four calorie values into an array
* Read the input string
* Initialize a variable to store total calories
* For each character in the string:

  * Convert it to an index using `ch - '1'`
  * Add the corresponding calorie value to the total
* Print the total

## Visual Walkthrough

### Test Case 1

Input

```
Calories: [1, 2, 3, 4]
String:   "1234"
```

Step-by-step addition

```
'1' → calories[0] = 1
'2' → calories[1] = 2
'3' → calories[2] = 3
'4' → calories[3] = 4
```

Total

```
10
```

---

### Test Case 2

Input

```
Calories: [4, 3, 2, 1]
String:   "12121"
```

Calculation

```
4 + 3 + 4 + 3 + 4 = 18
```

Result

```
18
```

## Complexity Analysis

### Time Complexity

**O(n)**
Each character in the string is processed once.

### Space Complexity

**O(1)**
Only a fixed-size array of four integers is used.

## Solution Explanation

The solution uses a direct mapping technique where each digit in the string corresponds to a specific calorie value.

By converting character digits to array indices and summing the values, the total calories are calculated efficiently without any complex logic or additional data structures.

## Full Solution

### C++ Implementation

```cpp
#include <iostream>
using namespace std;

int main() {

    // Array to store calorie values for squares 1 to 4
    int calories[4];

    // Variable to accumulate total calories burned
    int total = 0;

    // Read calorie values
    cin >> calories[0] >> calories[1] >> calories[2] >> calories[3];

    // Read the string representing steps taken
    string s;
    cin >> s;

    // Traverse each character in the string
    for (char ch : s) {

        // Convert character '1'-'4' to index 0-3
        // and add the corresponding calorie value
        total += calories[ch - '1'];
    }

    // Output the total calories burned
    cout << total;

    return 0;
}
```

## Test Cases Analysis

| Calories    | Steps | Total Calories |
| ----------- | ----- | -------------- |
| 1 2 3 4     | 1234  | 10             |
| 4 3 2 1     | 12121 | 18             |
| 10 10 10 10 | 4444  | 40             |
| 1 1 1 1     | 1111  | 4              |

## Edge Cases to Consider

* String contains only one character
* All characters are the same
* Maximum string length

## Common Test Cases

* Alternating digits
* Repeated digits
* Single digit repeated multiple times

## Common Mistakes to Avoid

* Incorrect character-to-index conversion
* Forgetting that characters `'1'`–`'4'` are not integers
* Using unnecessary conditional statements instead of direct mapping

## Interview Relevance

* Tests understanding of character arithmetic
* Evaluates efficient array usage
* Common example of mapping input to values

## What This Problem Teaches

* Using ASCII arithmetic for indexing
* Efficient accumulation techniques
* Leveraging constraints to simplify logic

## Key Takeaways

* Direct mapping often leads to the cleanest solutions
* Character arithmetic is powerful in C++
* Always align array indices with input representation

## Problem Difficulty Analysis

This is an **Easy-level** problem.
It focuses on basic array usage and string traversal, making it suitable for beginners and interview warm-ups.
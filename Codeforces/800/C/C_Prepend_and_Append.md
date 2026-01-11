# C. Prepend and Append

## Platform

Codeforces

## Problem Link

[https://codeforces.com/problemset/problem/1791/C](https://codeforces.com/problemset/problem/1791/C)

## Problem Statement

You are given a binary string `s` of length `n`.

You may repeatedly perform the following operation:

* Remove the **first** character and the **last** character of the string **if they are different**

Your task is to determine the **minimum possible length of the string** after performing the operation any number of times.

This process is applied independently for multiple test cases.

## Input Format

* The first line contains an integer `t` — the number of test cases
* For each test case:

  * An integer `n` — the length of the string
  * A binary string `s` of length `n`

## Output Format

For each test case, print a single integer representing the **minimum possible length** of the string.

## Constraints

* `1 ≤ t ≤ 10⁴`
* `1 ≤ n ≤ 2 × 10⁵`
* `s` consists only of characters `'0'` and `'1'`
* The sum of all `n` across test cases does not exceed `2 × 10⁵`

## Examples

### Example 1

Input

```
3
3
010
4
0110
5
01010
```

Explanation

* `"010"`
  First and last characters are the same → no removal
  Final length = `3`

* `"0110"`
  First = `'0'`, last = `'0'` → no removal
  Final length = `4`

* `"01010"`
  Remove `'0'` and `'1'`
  Remaining `"101"`
  Now ends are same → stop
  Final length = `3`

Output

```
3
4
3
```

### Example 2

Input

```
1
6
001011
```

Explanation

```
001011
remove 0 and 1 → 0101
remove 0 and 1 → 10
remove 1 and 0 → empty
```

Final length = `0`

Output

```
0
```

## Approach (Algorithm Type)

Two-pointer greedy string reduction.

## Intuition

The operation can only be applied **when the first and last characters differ**.

Instead of simulating string deletion, we can use two pointers:

* One starting at the beginning
* One starting at the end

As long as the characters at these pointers are different, they can be removed conceptually by moving the pointers inward.

Once the characters match, no further operation is possible.

## Algorithm Steps

* Read the number of test cases
* For each test case:

  * Read `n` and string `s`
  * Initialize two pointers:

    * `left = 0`
    * `right = n - 1`
  * While `left < right`:

    * If `s[left] == s[right]`, stop
    * Otherwise:

      * Increment `left`
      * Decrement `right`
  * The remaining string length is `right - left + 1`
  * Output this value

## Visual Walkthrough

Test Case 1:

```
s = "01010"
```

Pointer movement:

```
left=0 ('0'), right=4 ('0') → equal → stop
```

Final length:

```
4 - 0 + 1 = 5
```

---

Test Case 2:

```
s = "001011"
```

Steps:

```
0 != 1 → remove → left=1, right=4
0 != 1 → remove → left=2, right=3
1 != 0 → remove → left=3, right=2 (stop)
```

Final length:

```
0
```

---

Test Case 3:

```
s = "0110"
```

```
0 == 0 → stop immediately
```

Final length:

```
4
```

## Complexity Analysis

### Time Complexity

O(n) per test case
Each character is visited at most once by the two pointers.

### Space Complexity

O(1)
No additional data structures are used.

## Solution Explanation

The solution efficiently avoids modifying the string.

By comparing characters at symmetric positions using two pointers, it simulates the allowed removals in constant space.

Once matching characters are encountered at both ends, no further operations are allowed, and the remaining substring length is calculated directly.

## Full Solution (Heavily Commented C++ Code)

```cpp
#include <iostream>
using namespace std;

int main() {

    // Number of test cases
    int t;
    cin >> t;

    // Process each test case independently
    while (t--) {

        // Length of the string
        int n;
        cin >> n;

        // Binary string input
        string s;
        cin >> s;

        // Two pointers pointing to the start and end of the string
        int left = 0;
        int right = n - 1;

        // Continue removing characters while:
        // - pointers do not cross
        // - characters at both ends are different
        while (left < right) {

            // If both characters are the same,
            // no further removal is possible
            if (s[left] == s[right]) {
                break;
            }

            // Otherwise, simulate removal
            left++;
            right--;
        }

        // Remaining length of the string
        cout << right - left + 1 << '\n';
    }

    return 0;
}
```

## Test Cases Analysis

| String | Removals Performed | Final Length |
| ------ | ------------------ | ------------ |
| 010    | None               | 3            |
| 01010  | 1                  | 3            |
| 001011 | 3                  | 0            |
| 0110   | None               | 4            |

## Edge Cases to Consider

* String length is 1
* All characters are the same
* String becomes empty
* Large input size across multiple test cases

## Common Test Cases

* Alternating binary strings
* Palindromic binary strings
* Completely reducible strings

## Common Mistakes to Avoid

* Attempting to physically delete characters from the string
* Forgetting to stop when characters match
* Incorrect pointer boundary conditions

## Interview Relevance

* Demonstrates two-pointer technique
* Tests greedy decision-making
* Evaluates understanding of string manipulation constraints

## What This Problem Teaches

* Efficient simulation using pointers
* Avoiding unnecessary memory operations
* Leveraging problem constraints for optimization

## Key Takeaways

* Two pointers can replace costly string operations
* Stop conditions are critical in greedy algorithms
* Always compute results directly when possible

## Problem Difficulty Analysis

This is a **Medium-level** problem.
While the logic is simple, recognizing that the operation can be simulated without modifying the string is the key insight.
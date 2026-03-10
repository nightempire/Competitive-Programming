# C_Clock_Conversion

## Platform

Codeforces

## Problem Link

[C. Clock Conversion](https://codeforces.com/problemset/problem/1950/C)

## Problem Statement

You are given a time in **24-hour format** (`HH:MM`).
Your task is to convert it into the **12-hour format** with the appropriate **AM or PM** suffix.

Rules for conversion:

* `00:00` to `11:59` → **AM**
* `12:00` to `23:59` → **PM**
* Hour `00` should be converted to `12`.
* Hour values greater than `12` should subtract `12`.

The minutes remain unchanged.

For each test case, output the converted time in **12-hour format** followed by `"AM"` or `"PM"`.

## Input Format

* The first line contains an integer `t` — the number of test cases.
* Each of the next `t` lines contains a string representing time in the format:

```
HH:MM
```

## Output Format

For each test case, print the converted time in the format:

```
HH:MM AM
```

or

```
HH:MM PM
```

## Constraints

* `1 ≤ t ≤ 100`
* Time format always follows `HH:MM`
* `00 ≤ HH ≤ 23`
* `00 ≤ MM ≤ 59`

## Examples

### Example 1

Input

```
3
00:00
12:30
23:15
```

Explanation

Case 1:

```
00:00 → 12:00 AM
```

Case 2:

```
12:30 → 12:30 PM
```

Case 3:

```
23:15 → 11:15 PM
```

Output

```
12:00 AM
12:30 PM
11:15 PM
```

---

### Example 2

Input

```
2
09:45
15:20
```

Explanation

Case 1:

```
09:45 → 09:45 AM
```

Case 2:

```
15:20 → 03:20 PM
```

Output

```
09:45 AM
03:20 PM
```

---

### Example 3

Input

```
2
11:59
13:05
```

Explanation

Case 1:

```
11:59 → 11:59 AM
```

Case 2:

```
13:05 → 01:05 PM
```

Output

```
11:59 AM
01:05 PM
```

## Approach

String Parsing with Conditional Time Conversion

## Intuition

The hour component determines whether the time is **AM or PM**.

Key observations:

* `00` hours correspond to **12 AM**.
* `01` to `11` remain unchanged and are **AM**.
* `12` remains `12` but is **PM**.
* `13` to `23` must subtract `12` and become **PM**.

Since the input is given as a string (`HH:MM`), we extract the first two characters to compute the hour.

The minutes portion remains unchanged.

## Algorithm Steps

* Read integer `t`.
* For each test case:

  * Read time string `s`.
  * Extract the hour value from the first two characters.
  * If `hour < 12`:

    * If `hour == 0`:

      * Replace hour with `12`.
    * Print `"AM"`.
  * Otherwise (`hour ≥ 12`):

    * If `hour > 12`:

      * Subtract `12`.
      * Update the hour digits in the string.
    * Print `"PM"`.

## Visual Walkthrough

### Test Case 1

Input

```
00:45
```

Extract hour:

```
00
```

Conversion:

```
00 → 12 AM
```

Result:

```
12:45 AM
```

---

### Test Case 2

Input

```
15:20
```

Extract hour:

```
15
```

Conversion:

```
15 - 12 = 3
```

Result:

```
03:20 PM
```

---

### Test Case 3

Input

```
12:30
```

Extract hour:

```
12
```

Rule:

```
12 remains 12 but becomes PM
```

Result:

```
12:30 PM
```

## Complexity Analysis

### Time Complexity

O(t)

Each test case performs constant-time operations on the string.

### Space Complexity

O(1)

Only a few variables are used per test case.

## Solution Explanation

The program reads the time as a string and converts the hour portion into an integer.

Based on the hour:

* It determines whether the time is AM or PM.
* It modifies the hour portion of the string if necessary.

Finally, it prints the updated string along with the appropriate suffix.

This approach avoids unnecessary parsing of minutes and keeps the solution efficient.

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

        // Time string in HH:MM format
        string s;
        cin >> s;

        // Extract hour from the string
        int hour = (s[0] - '0') * 10 + (s[1] - '0');

        // If time is in AM range
        if (hour < 12) {

            // Special case: 00 -> 12 AM
            if (hour == 0) {
                s[0] = '1';
                s[1] = '2';
            }

            // Print time with AM
            cout << s << " AM\n";

        } else {

            // If hour is greater than 12
            if (hour != 12) {

                // Convert to 12-hour format
                hour -= 12;

                // Update the hour digits
                s[0] = '0' + hour / 10;
                s[1] = '0' + hour % 10;
            }

            // Print time with PM
            cout << s << " PM\n";
        }
    }

    return 0;
}
```

## Test Cases Analysis

| Input | Converted Time |
| ----- | -------------- |
| 00:00 | 12:00 AM       |
| 09:30 | 09:30 AM       |
| 12:45 | 12:45 PM       |
| 15:10 | 03:10 PM       |
| 23:59 | 11:59 PM       |

## Edge Cases to Consider

* Midnight (`00:00`)
* Noon (`12:00`)
* Hour values just before and after noon
* Leading zero hours (`01`, `02`, etc.)

## Common Test Cases

* `00:00`
* `11:59`
* `12:00`
* `13:30`
* `23:45`

## Common Mistakes to Avoid

* Forgetting to convert `00` to `12 AM`
* Incorrectly converting `12` to `00`
* Modifying the minute portion unintentionally

## Interview Relevance

* Tests string parsing and manipulation
* Reinforces conditional logic
* Demonstrates handling of time format conversions

## What This Problem Teaches

* Extracting numeric values from strings
* Formatting output properly
* Handling edge cases in time conversion

## Key Takeaways

* Time conversions require careful handling of edge cases
* String manipulation can simplify formatting problems
* Always verify boundary values such as `00` and `12`

## Problem Difficulty Analysis

This is an **Easy-level** problem.

It mainly involves basic string processing and conditional checks, making it a straightforward implementation task suitable for beginners in competitive programming.
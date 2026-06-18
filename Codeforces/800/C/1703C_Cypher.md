# C. Cypher

## Platform

Codeforces

## Problem Link

[C. Cypher - Codeforces Problem 1703C](https://codeforces.com/problemset/problem/1703/C?utm_source=chatgpt.com)

## Problem Statement

There are `n` wheels on a cypher lock. Each wheel initially displays a digit from `0` to `9`.

For each wheel, a sequence of operations is provided:

* `D` means rotate the wheel downward, increasing the digit by `1`.
* `U` means rotate the wheel upward, decreasing the digit by `1`.

The digits wrap around cyclically:

* After `9` comes `0`.
* Before `0` comes `9`.

For every wheel, apply all given operations in order and determine the final digit displayed.

## Input Format

* The first line contains an integer `t` — the number of test cases.
* For each test case:

  * The first line contains an integer `n` — the number of wheels.
  * The second line contains `n` integers representing the initial digits.
  * The next `n` lines describe the operations for each wheel:

    * An integer `m` — the length of the operation sequence.
    * A string `s` of length `m` consisting only of `U` and `D`.

## Output Format

For each test case, print `n` integers representing the final digits on the wheels after all operations have been applied.

## Constraints

* `1 ≤ t ≤ 100`
* `1 ≤ n ≤ 100`
* `0 ≤ digit ≤ 9`
* `1 ≤ m ≤ 10`
* `s` contains only `U` and `D`

## Examples

### Example 1

Input

```text
1
3
0 1 2
3 DDD
2 UU
1 D
```

Output

```text
3 9 3
```

### Explanation

Wheel 1:

```text
0 → 1 → 2 → 3
```

Final digit:

```text
3
```

Wheel 2:

```text
1 → 0 → 9
```

Final digit:

```text
9
```

Wheel 3:

```text
2 → 3
```

Final digit:

```text
3
```

---

### Example 2

Input

```text
1
2
9 0
1 D
1 U
```

Output

```text
0 9
```

### Explanation

Wheel 1:

```text
9 → 0
```

Wheel 2:

```text
0 → 9
```

Both operations demonstrate cyclic wrapping.

---

### Example 3

Input

```text
1
1
5
4 UUDD
```

Output

```text
5
```

### Explanation

Operations:

```text
5 → 4 → 3 → 4 → 5
```

The wheel returns to its original value.

## Approach

### Algorithm Type

Simulation with Cyclic Digit Manipulation

## Intuition

Each wheel operates independently.

For every wheel:

* Process the operation string character by character.
* `D` increases the digit.
* `U` decreases the digit.
* Whenever the digit exceeds `9`, it wraps back to `0`.
* Whenever the digit becomes less than `0`, it wraps back to `9`.

The given solution performs this simulation directly.

## Algorithm Steps

* Read the number of test cases.
* For each test case:

  * Read `n`.
  * Read the initial digits of all wheels.
  * For every wheel:

    * Read `m` and operation string `s`.
    * Traverse each character:

      * If character is `D`, increment the digit.
      * If character is `U`, decrement the digit.
      * Handle wrap-around appropriately.
  * Output the final digit of every wheel.

## Visual Walkthrough

### Test Case 1

Initial wheel:

```text
Digit = 0
Operations = DDD
```

Simulation:

```text
0 → 1 → 2 → 3
```

Final digit:

```text
3
```

---

### Test Case 2

Initial wheel:

```text
Digit = 0
Operations = U
```

Simulation:

```text
0 → 9
```

Wrap-around occurs because the digit goes below zero.

Final digit:

```text
9
```

---

### Test Case 3

Initial wheel:

```text
Digit = 9
Operations = D
```

Simulation:

```text
9 → 10
```

Applying modulo:

```text
10 % 10 = 0
```

Final digit:

```text
0
```

## Complexity Analysis

### Time Complexity

**O(n × m)**

For each wheel:

* Every operation in its command string is processed exactly once.

Therefore:

```text
Time Complexity = O(total operations)
```

Since `m ≤ 10`, the solution is extremely efficient.

### Space Complexity

**O(n)**

The solution stores:

* Initial wheel digits.
* Operation strings.

Hence:

```text
O(n)
```

additional space is used.

## Solution Explanation

The solution first stores the initial value of every wheel.

For each wheel:

* Character `D` increases the digit.
* Character `U` decreases the digit.
* When decrementing from `0`, the digit becomes `9`.
* Increment operations may temporarily create values greater than `9`, and the final modulo operation converts them back into the valid range.

After processing all commands, every wheel's value is printed modulo `10`, ensuring digits remain between `0` and `9`.

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

        // Number of wheels
        int n;
        cin >> n;

        // Store current value of each wheel
        int wheels[n];

        // Read initial wheel values
        for(int i = 0; i < n; i++) {
            cin >> wheels[i];
        }

        // Process each wheel independently
        for(int i = 0; i < n; i++) {

            int m;
            string s;

            // Length of operation string and operations
            cin >> m >> s;

            // Apply all operations in order
            for(char ch : s) {

                // Down operation increases digit
                if(ch == 'D') {
                    wheels[i]++;
                }

                // Up operation decreases digit
                else if(wheels[i] == 0) {
                    wheels[i] = 9;
                }

                else {
                    wheels[i]--;
                }
            }
        }

        // Print final wheel values
        for(int wheel : wheels) {
            cout << wheel % 10 << ' ';
        }

        cout << '\n';
    }

    return 0;
}
```

## Test Cases Analysis

| Initial Digit | Operations | Simulation        | Final Digit |
| ------------- | ---------- | ----------------- | ----------- |
| 0             | DDD        | 0 → 1 → 2 → 3     | 3           |
| 1             | UU         | 1 → 0 → 9         | 9           |
| 9             | D          | 9 → 10 → 0        | 0           |
| 5             | UUDD       | 5 → 4 → 3 → 4 → 5 | 5           |
| 0             | UUU        | 0 → 9 → 8 → 7     | 7           |

## Edge Cases to Consider

* Initial digit is `0` and operation is `U`.
* Initial digit is `9` and operation is `D`.
* Multiple consecutive wrap-arounds.
* Wheel receives only `U` operations.
* Wheel receives only `D` operations.
* Single wheel (`n = 1`).

## Common Test Cases

### Wrap Around Upward

```text
Input:
1
1
0
1 U

Output:
9
```

---

### Wrap Around Downward

```text
Input:
1
1
9
1 D

Output:
0
```

---

### No Net Change

```text
Input:
1
1
5
4 UUDD

Output:
5
```

## Common Mistakes to Avoid

* Forgetting that digits wrap around cyclically.
* Applying modulo after every decrement without handling negative values correctly.
* Processing operation strings for the wrong wheel.

## Interview Relevance

* Demonstrates simulation-based problem solving.
* Tests handling of cyclic state transitions.
* Reinforces careful implementation of wrap-around logic.

## What This Problem Teaches

* Direct simulation techniques.
* Circular number systems.
* Processing independent state transitions efficiently.

## Key Takeaways

* Cyclic values are often handled using wrap-around logic.
* Simulation problems become easy when each state transition is processed sequentially.
* Careful handling of boundary values (`0` and `9`) is crucial.

## Problem Difficulty Analysis

This is an **Easy** implementation and simulation problem.

The main task is correctly applying a sequence of cyclic digit transformations. No advanced data structures or algorithms are required; careful handling of wrap-around behavior is sufficient for an accepted solution.
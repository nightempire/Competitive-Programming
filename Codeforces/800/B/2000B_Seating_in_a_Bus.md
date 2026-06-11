# B. Seating in a Bus

## Platform

Codeforces

## Problem Link

[B. Seating in a Bus - Codeforces Problem 2000B](https://codeforces.com/problemset/problem/2000/B?utm_source=chatgpt.com)

## Problem Statement

A bus contains `n` seats arranged in a single row and numbered consecutively.

Passengers enter the bus one by one in a given order and occupy the seats specified in the input.

The seating arrangement is considered valid if every passenger after the first chooses a seat that is directly adjacent to at least one already occupied seat.

For each test case, determine whether the given seating order is valid.

Print:

* `"YES"` if the seating order is valid.
* `"NO"` otherwise.

## Input Format

* The first line contains an integer `t` — the number of test cases.
* For each test case:

  * The first line contains an integer `n` — the number of passengers (and seats occupied).
  * The second line contains `n` integers representing the order in which seats are occupied.

## Output Format

For each test case, print:

* `"YES"` if the seating process is valid.
* `"NO"` otherwise.

Each answer should be printed on a new line.

## Constraints

* `1 ≤ t ≤ 10^4`
* `1 ≤ n ≤ 10^5`
* Seat numbers form a permutation of integers from `1` to `n`.
* Sum of `n` over all test cases does not exceed the contest limit.

## Examples

### Example 1

Input

```text
1
4
2 1 3 4
```

Output

```text
YES
```

### Explanation

Passenger seating order:

```text
Seat 2 occupied first
```

Current occupied segment:

```text
[2]
```

Next passenger:

```text
Seat 1
```

Seat 1 is adjacent to seat 2.

Occupied segment:

```text
[1, 2]
```

Next passenger:

```text
Seat 3
```

Adjacent to seat 2.

Occupied segment:

```text
[1, 2, 3]
```

Next passenger:

```text
Seat 4
```

Adjacent to seat 3.

All passengers satisfy the condition.

Result:

```text
YES
```

---

### Example 2

Input

```text
1
4
2 4 1 3
```

Output

```text
NO
```

### Explanation

First passenger occupies seat 2.

Occupied seats:

```text
[2]
```

Second passenger chooses seat 4.

Seat 4 is not adjacent to any occupied seat.

Therefore the arrangement becomes invalid immediately.

Result:

```text
NO
```

---

### Example 3

Input

```text
1
5
3 2 4 1 5
```

Output

```text
YES
```

### Explanation

Seating progression:

```text
3
```

```text
2 3
```

```text
2 3 4
```

```text
1 2 3 4
```

```text
1 2 3 4 5
```

Each newly occupied seat extends the occupied block from either side.

Result:

```text
YES
```

## Approach

### Algorithm Type

Contiguous Occupied Segment Simulation

## Intuition

After the first passenger sits down, the occupied seats form a contiguous segment.

Let:

* `left` = leftmost occupied seat
* `right` = rightmost occupied seat

For every new passenger, the chosen seat must extend the occupied segment by exactly one position:

* Either `left - 1`
* Or `right + 1`

If a passenger chooses any other seat, then that seat is not adjacent to the current occupied block, making the arrangement invalid.

Thus, we only need to maintain the current boundaries of the occupied segment.

## Algorithm Steps

* Read the number of test cases `t`.
* For each test case:

  * Read `n`.
  * Read the first occupied seat.
  * Initialize:

    * `left = first seat`
    * `right = first seat`
    * `flag = true`
  * For each remaining seat:

    * Read the seat number.
    * If it equals `left - 1`:

      * Expand the segment to the left.
    * Else if it equals `right + 1`:

      * Expand the segment to the right.
    * Otherwise:

      * Mark arrangement as invalid.
  * Print `"YES"` if valid, otherwise `"NO"`.

## Visual Walkthrough

### Test Case 1

Input sequence:

```text
2 1 3 4
```

Initially:

```text
left = right = 2
```

After seat 1:

```text
1 2
^   ^
L   R
```

After seat 3:

```text
1 2 3
^     ^
L     R
```

After seat 4:

```text
1 2 3 4
^       ^
L       R
```

Valid arrangement.

Output:

```text
YES
```

---

### Test Case 2

Input sequence:

```text
2 4 1 3
```

Initially:

```text
[2]
```

Next seat:

```text
4
```

Required seats:

```text
1 or 3
```

Since seat 4 is neither, the arrangement becomes invalid.

Output:

```text
NO
```

---

### Test Case 3

Input sequence:

```text
3 2 4 1 5
```

Progression:

```text
3
```

```text
2 3
```

```text
2 3 4
```

```text
1 2 3 4
```

```text
1 2 3 4 5
```

Every new passenger extends the occupied segment.

Output:

```text
YES
```

## Complexity Analysis

### Time Complexity

**O(n)** per test case

Each seat is processed exactly once.

```text
Total Operations = n
```

Therefore:

```text
O(n)
```

### Space Complexity

**O(1)**

The algorithm only stores:

* `left`
* `right`
* `flag`

No additional data structures are used.

Therefore:

```text
O(1)
```

## Solution Explanation

The solution maintains the current occupied continuous segment using two boundary variables:

* `left`
* `right`

Initially, both point to the first occupied seat.

For every subsequent passenger:

* If the seat is immediately left of the segment (`left - 1`), expand left.
* If the seat is immediately right of the segment (`right + 1`), expand right.
* Otherwise, the passenger is not sitting adjacent to any occupied seat, making the arrangement invalid.

After processing all passengers, the validity flag determines the answer.

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

        // Number of passengers/seats
        int n;

        // Boundaries of the occupied segment
        int left, right;

        cin >> n >> left;

        // Initially only the first seat is occupied
        left = right = left;

        // Indicates whether the seating order remains valid
        bool flag = true;

        // Process remaining passengers
        for(int i = 1; i < n; i++) {

            int num;
            cin >> num;

            // Extend occupied segment to the left
            if(left > 0 && num == left - 1) {
                left--;
            }

            // Extend occupied segment to the right
            else if(right < n && num == right + 1) {
                right++;
            }

            // Any other seat breaks the adjacency rule
            else {
                flag = false;
            }
        }

        // Print result for current test case
        cout << (flag ? "YES\n" : "NO\n");
    }

    return 0;
}
```

## Test Cases Analysis

| Input Sequence | Segment Expansion        | Result |
| -------------- | ------------------------ | ------ |
| 2 1 3 4        | Left, Right, Right       | YES    |
| 2 4 1 3        | Invalid at seat 4        | NO     |
| 3 2 4 1 5      | Left, Right, Left, Right | YES    |
| 1              | Single passenger         | YES    |
| 4 3 1 2 4      | Invalid at seat 1        | NO     |

## Edge Cases to Consider

* Only one passenger (`n = 1`)
* First seat occupied is seat `1`
* First seat occupied is seat `n`
* Continuous expansion only on the left side
* Continuous expansion only on the right side
* Invalid seat chosen immediately after the first passenger

## Common Test Cases

### Single Passenger

```text
1
1
1
```

Output

```text
YES
```

---

### Immediate Violation

```text
1
4
2 4 1 3
```

Output

```text
NO
```

---

### Valid Left-Right Expansion

```text
1
5
3 2 4 1 5
```

Output

```text
YES
```

## Common Mistakes to Avoid

* Checking adjacency against all occupied seats instead of maintaining segment boundaries.
* Forgetting to update `left` and `right` after a valid expansion.
* Assuming any unoccupied seat can be chosen as long as it exists.

## Interview Relevance

* Demonstrates interval and boundary management.
* Tests simulation and state-tracking skills.
* Highlights how maintaining minimal information can replace larger data structures.

## What This Problem Teaches

* Simulation of sequential processes.
* Maintaining a contiguous interval efficiently.
* Converting an adjacency condition into simple boundary updates.

## Key Takeaways

* A contiguous occupied block can be represented using only two boundaries.
* Expanding intervals is often more efficient than storing all elements.
* Careful observation can reduce a seemingly complex simulation to a simple O(n) solution.

## Problem Difficulty Analysis

This is an **Easy-to-Medium** implementation problem.

The main challenge is recognizing that occupied seats always form a single contiguous segment. Once this observation is made, the problem can be solved using only two boundary variables and a straightforward simulation, resulting in an efficient **O(n)** solution.
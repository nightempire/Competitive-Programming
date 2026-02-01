# B_Triple

## Platform

Codeforces

## Problem Link

[B. Triple](https://codeforces.com/problemset/problem/1669/B)

## Problem Statement

You are given multiple test cases.
For each test case, you are given an array of integers.

Your task is to determine whether there exists **any integer that appears at least three times** in the array.

* If such an integer exists, print **any one** of them.
* Otherwise, print `-1`.

## Input Format

* The first line contains an integer `t` — the number of test cases.
* For each test case:

  * The first line contains an integer `n` — the size of the array.
  * The second line contains `n` integers representing the array elements.

## Output Format

* For each test case:

  * Print an integer that appears **at least three times**, or
  * Print `-1` if no such integer exists.

Each output should be printed on a new line.

## Constraints

* `1 ≤ t ≤ 100`
* `1 ≤ n ≤ 2 × 10⁵`
* `1 ≤ array[i] ≤ 10⁹`
* Sum of `n` over all test cases does not exceed `2 × 10⁵`

## Examples

### Example 1

Input

```
3
5
1 2 2 3 2
4
1 2 3 4
6
5 5 5 5 1 2
```

Explanation

* Test case 1:

  * `2` appears three times → valid answer
* Test case 2:

  * No number appears three times → output `-1`
* Test case 3:

  * `5` appears four times → valid answer

Output

```
2
-1
5
```

---

### Example 2

Input

```
1
3
7 7 7
```

Explanation
The number `7` appears exactly three times.

Output

```
7
```

## Approach

Frequency counting using a hash-based map.

## Intuition

To determine whether any number appears at least three times, we must:

* Count how many times each number occurs
* Check if **any frequency is greater than or equal to three**

Using a map allows us to track frequencies efficiently while iterating through the array once.

## Algorithm Steps

* Read the number of test cases `t`
* For each test case:

  * Read `n`
  * Initialize a map to store frequency counts
  * Read each number and increment its frequency in the map
  * Traverse the map:

    * If any number has frequency ≥ 3, print that number and stop
  * If no such number is found, print `-1`

## Visual Walkthrough

### Case 1

```
Array: [1, 2, 2, 3, 2]
```

Frequency table:

```
1 → 1
2 → 3
3 → 1
```

Decision:

```
2 appears ≥ 3 times → output 2
```

---

### Case 2

```
Array: [1, 2, 3, 4]
```

Frequency table:

```
Each element → 1
```

Decision:

```
No frequency ≥ 3 → output -1
```

---

### Case 3

```
Array: [5, 5, 5, 5, 1, 2]
```

Frequency table:

```
5 → 4
1 → 1
2 → 1
```

Decision:

```
5 appears ≥ 3 times → output 5
```

## Complexity Analysis

### Time Complexity

**O(n log n)**

* Each insertion/update in a map takes `O(log n)`
* Total of `n` insertions per test case

### Space Complexity

**O(n)**

* The map stores up to `n` distinct elements in the worst case

## Solution Explanation

The solution counts occurrences of each number using a map.
Once all frequencies are known, it scans the map to find any number whose count is at least three.
If found, that number is printed immediately; otherwise, `-1` is returned.

This approach is simple, readable, and efficient within the given constraints.

## Full Solution

### C++ Implementation

```cpp
#include <iostream>
#include <map>
using namespace std;

int main() {

    // Number of test cases
    int t;
    cin >> t;

    // Process each test case
    while(t--) {

        // Size of the array
        int n;
        cin >> n;

        // Map to store frequency of each number
        map<int, int> m;

        // Read array elements and count frequencies
        for(int i = 0; i < n; i++) {
            int num;
            cin >> num;
            m[num]++;
        }

        // Flag to check if a valid number is found
        bool flag = false;

        // Iterate over the map to find any number with frequency >= 3
        for(pair<int, int> p : m) {

            // If the number appears at least three times
            if(p.second >= 3) {

                // Print the number
                cout << p.first << '\n';

                // Mark as found
                flag = true;
                break;
            }
        }

        // If no such number exists, print -1
        if(!flag)
            cout << "-1\n";
    }

    return 0;
}
```

## Test Cases Analysis

| Input Array     | Frequency Match | Output |
| --------------- | --------------- | ------ |
| `[1,2,2,3,2]`   | `2 → 3`         | `2`    |
| `[1,2,3,4]`     | None            | `-1`   |
| `[5,5,5,5,1,2]` | `5 → 4`         | `5`    |
| `[7,7,7]`       | `7 → 3`         | `7`    |

## Edge Cases to Consider

* Minimum array size
* All elements distinct
* One element appearing more than three times

## Common Test Cases

* Exactly three repetitions
* More than three repetitions
* No valid repetitions

## Common Mistakes to Avoid

* Forgetting to reset the map for each test case
* Using incorrect frequency comparison (`> 3` instead of `>= 3`)
* Printing multiple answers instead of stopping after the first valid one

## Interview Relevance

* Tests frequency counting techniques
* Evaluates understanding of maps and iteration
* Common pattern in array-based interview problems

## What This Problem Teaches

* Efficient use of hash maps for counting
* Translating problem constraints into frequency logic
* Early termination for optimized performance

## Key Takeaways

* Frequency maps simplify repetition-based problems
* Always check constraints before choosing data structures
* Clean logic improves readability and correctness

## Problem Difficulty Analysis

This is an **Easy-level** problem.

It focuses on basic data structures and counting logic, making it ideal for beginners and commonly asked in coding interviews as a warm-up problem.
# A_Doremy_s_Paint_3

## Platform

Codeforces

## Problem Link

[A. Doremy’s Paint 3](https://codeforces.com/problemset/problem/1890/A)

## Problem Statement

You are given multiple test cases.
In each test case:

* An integer `n` — the number of paint pieces.
* A list of `n` integers representing paint labels.

Doremy wants to arrange paint pieces into a valid pattern.

The paint arrangement is considered **valid** if:

* All paint pieces are identical, or
* There are exactly two distinct labels, and one label appears `ceil(n/2)` times and the other appears `floor(n/2)` times.

Your task is to determine whether the given paint arrangement is valid.

Print `"Yes"` if valid, otherwise print `"No"`.

## Input Format

* The first line contains an integer `t`, the number of test cases.
* For each test case:

  * The first line contains an integer `n`
  * The second line contains `n` integers — labels of paint pieces

## Output Format

For each test case, print:

* `"Yes"` if the arrangement is valid
* `"No"` otherwise

Each answer should be printed on a new line.

## Constraints

* `1 ≤ t ≤ 10^4`
* `1 ≤ n ≤ 10^5`
* Sum of `n` over all test cases does not exceed limits
* `1 ≤ label ≤ 10^9`

## Examples

### Example 1

Input

```
3
3
1 1 1
4
1 1 2 2
5
1 1 2 2 2
```

Explanation

* Test case 1:

  * All paint labels are the same → valid
* Test case 2:

  * Two labels, each appears `2` times →
    `ceil(4/2)=2`, `floor(4/2)=2` → valid
* Test case 3:

  * Counts → label `1`: 2, label `2`: 3
    `ceil(5/2)=3`, `floor(5/2)=2` → valid

Output

```
Yes
Yes
Yes
```

### Example 2

Input

```
2
3
1 2 3
6
1 1 1 2 2 3
```

Explanation

* Test case 1:

  * 3 distinct labels → invalid
* Test case 2:

  * 3 distinct labels → invalid

Output

```
No
No
```

## Approach

**Count unique labels and their frequencies**

## Intuition

After sorting the labels, group them into distinct values with frequency counts.

Valid scenarios:

* Only one distinct label (all pieces are the same)
* Two distinct labels with frequencies exactly:

  * one label has `ceil(n/2)` occurrences
  * the other has `floor(n/2)` occurrences

Any other distribution is invalid.

## Algorithm Steps

* Read integer `t`
* For each test case:

  * Read `n` and the array `a`
  * Sort the array
  * Create a list of `(label, count)` pairs
  * If exactly 1 distinct label → `Yes`
  * Else if exactly 2 distinct labels:

    * Let `oddCnt = ceil(n/2)`
    * Let `evenCnt = floor(n/2)`
    * If frequencies match `(oddCnt, evenCnt)` in any order → `Yes`
    * Else → `No`
  * Otherwise → `No`

## Visual Walkthrough

### Test Case 1

Input:

```
[1, 1, 1]
```

Distinct labels: `{1}`
Count: `3`
Valid → `"Yes"`

---

### Test Case 2

Input:

```
[1, 1, 2, 2]
```

Distinct labels and counts:

```
1:2, 2:2
```

`ceil(4/2)=2`, `floor(4/2)=2` → Valid → `"Yes"`

---

### Test Case 3

Input:

```
[1,2,3]
```

Distinct > 2 → Invalid → `"No"`

## Complexity Analysis

### Time Complexity

**O(n log n)** per test case due to sorting
Frequency collection and checking are linear.

### Space Complexity

**O(n)** auxiliary space for counts

## Solution Explanation

The core idea is to verify whether the array has either:

* Only one distinct value (trivially valid), or
* Exactly two distinct values with balanced frequencies matching half splits.

Using sorting allows grouping identical values and computing frequencies efficiently.

The balanced frequency requirement ensures one label fills the larger half (`ceil(n/2)`) and the other fills the smaller half (`floor(n/2)`).

## Full Solution

### C++ Implementation

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

int main() {

    int t;
    cin >> t;
    while (t--) {
        int n;
        cin >> n;
        vector<int> a(n);
        for (int &x : a)
            cin >> x;

        // Sort to group equal values
        sort(a.begin(), a.end());

        // Collect (value, frequency) pairs
        vector<pair<int, int>> freq;
        for (int i = 0; i < n; ) {
            int j = i;
            while (j < n && a[j] == a[i]) {
                j++;
            }
            freq.push_back({a[i], j - i});
            i = j;
        }

        // If only one unique label → always valid
        if (freq.size() == 1) {
            cout << "Yes\n";
        }
        // If exactly two unique labels → check frequency pattern
        else if (freq.size() == 2) {
            int oddCnt = (n + 1) / 2;
            int evenCnt = n / 2;

            bool ok = false;
            if (freq[0].second == oddCnt && freq[1].second == evenCnt)
                ok = true;
            if (freq[0].second == evenCnt && freq[1].second == oddCnt)
                ok = true;

            cout << (ok ? "Yes\n" : "No\n");
        }
        else {
            cout << "No\n";
        }
    }
    return 0;
}
```

## Test Cases Analysis

| Test Case | Input Values    | Distinct | Frequencies | Valid |
| --------- | --------------- | -------- | ----------- | ----- |
| 1         | 1 1 1           | 1        | [3]         | Yes   |
| 2         | 1 1 2 2         | 2        | [2,2]       | Yes   |
| 3         | 1 1 2 2 2       | 2        | [2,3]       | Yes   |
| 4         | 1 2 3           | 3        | [1,1,1]     | No    |
| 5         | 1 1 1 1 2 2 3 3 | 3        | [4,2,2]     | No    |

## Edge Cases to Consider

* All elements identical
* Exactly two distinct values with balanced counts
* More than two distinct values

## Common Test Cases

* Small arrays with minimal distinct values
* Large arrays where one value dominates half
* Multiple distinct values beyond two

## Common Mistakes to Avoid

* Not handling both ordering cases of the two frequencies
* Forgetting to sort before counting
* Incorrect ceiling and floor calculation

## Interview Relevance

* Tests grouping and frequency counting
* Uses sorting and conditional logic
* Balanced classification checking

## What This Problem Teaches

* How to derive conditions from frequency patterns
* Using sorting to simplify grouping tasks
* Distinguishing between single and double label distributions

## Key Takeaways

* Frequency patterns can encode valid configurations
* Sorting+grouping is a powerful technique
* Exact count matching is essential for validity

## Problem Difficulty Analysis

This is an **Easy-to-Medium** level problem.
Understanding frequency patterns and simple condition checks are crucial to solving it correctly.
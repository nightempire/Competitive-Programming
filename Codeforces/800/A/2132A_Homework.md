## Platform

Codeforces

## Problem Link

[A. Homework](https://codeforces.com/problemset/problem/2132/A)

---

## Problem Statement

You are given:

* A string `a` of length `n`
* A string `b` of length `m`
* A string `c` of length `m`, consisting of characters `'V'` and `'H'`

You must perform `m` operations sequentially.

For each index `i` (from `0` to `m-1`):

* If `c[i] == 'V'`:

  * Add character `b[i]` **to the front** of string `a`
* If `c[i] == 'H'`:

  * Add character `b[i]` **to the end** of string `a`

After performing all operations, output the final string `a`.

---

## Input Format

* The first line contains an integer `t` — number of test cases
* For each test case:

  * Integer `n`, string `a`
  * Integer `m`, string `b`, string `c`

---

## Output Format

For each test case:

* Print the final string after all operations

---

## Constraints

* `1 ≤ t ≤ 100`
* `1 ≤ n, m ≤ 100`
* Strings consist of lowercase English letters

---

## Examples

### Example 1

Input

```id="k4x2pn"
1
3 abc
3 xyz
VHV
```

Explanation

Operations:

* i = 0 → `V` → prepend `x` → `xabc`
* i = 1 → `H` → append `y` → `xabcy`
* i = 2 → `V` → prepend `z` → `zxabcy`

Output

```id="t9m7vl"
zxabcy
```

---

### Example 2

Input

```id="p6y3mx"
1
1 a
4 bcde
HHVV
```

Explanation

* Append `b` → `ab`
* Append `c` → `abc`
* Prepend `d` → `dabc`
* Prepend `e` → `edabc`

Output

```id="u2r8ks"
edabc
```

---

### Example 3

Input

```id="w7z4qd"
1
2 ab
2 cd
VV
```

Explanation

* Prepend `c` → `cab`
* Prepend `d` → `dcab`

Output

```id="y3l9mf"
dcab
```

---

## Approach

Simulation with string concatenation

---

## Intuition

Each operation modifies the string `a` by:

* Adding a character at the **front**, or
* Adding a character at the **end**

Since operations are sequential, we must apply them in order.

---

## Algorithm Steps

* Read `t`
* For each test case:

  * Read `n`, `a`
  * Read `m`, `b`, `c`
  * For `i` from `0` to `m-1`:

    * If `c[i] == 'V'`:

      * `a = b[i] + a`
    * Else:

      * `a = a + b[i]`
  * Print final `a`

---

## Visual Walkthrough

### Case 1

```id="n8p3xv"
a = abc
b = xyz
c = VHV

Step 1: x + abc → xabc
Step 2: xabc + y → xabcy
Step 3: z + xabcy → zxabcy
```

---

### Case 2

```id="h4v2mz"
a = a
b = bcde
c = HHVV

→ ab
→ abc
→ dabc
→ edabc
```

---

### Case 3

```id="k1t7qx"
a = ab
b = cd
c = VV

→ cab
→ dcab
```

---

## Complexity Analysis

### Time Complexity

O(n + m²)

* Each prepend operation shifts the string → costly
* Worst case: repeated front insertions

---

### Space Complexity

O(n + m)

* Final string size grows to `n + m`

---

## Solution Explanation

The solution directly simulates the process:

* For each operation:

  * Modify the string accordingly
* Since constraints are small (`≤ 100`), this approach is efficient enough

---

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

        // Initial string
        int n, m;
        string a, b, c;

        cin >> n >> a;
        cin >> m >> b >> c;

        // Perform operations
        for(int i = 0; i < m; i++) {

            // If 'V' → prepend
            if(c[i] == 'V') {
                a = b[i] + a;
            }

            // If 'H' → append
            else {
                a += b[i];
            }
        }

        // Output final string
        cout << a << '\n';
    }

    return 0;
}
```

---

## Test Cases Analysis

| a   | b    | c    | Result |
| --- | ---- | ---- | ------ |
| abc | xyz  | VHV  | zxabcy |
| a   | bcde | HHVV | edabc  |
| ab  | cd   | VV   | dcab   |

---

## Edge Cases to Consider

* `m = 0` → no changes
* All operations are prepend
* All operations are append
* Single character strings

---

## Common Test Cases

* Only prepend operations
* Only append operations
* Mixed operations

---

## Common Mistakes to Avoid

* Incorrect order of operations
* Mixing prepend and append logic
* Not handling string concatenation correctly

---

## Interview Relevance

* String manipulation
* Simulation problems
* Understanding operation sequences

---

## What This Problem Teaches

* Sequential processing of operations
* String building techniques
* Handling front and back insertions

---

## Key Takeaways

* Order of operations matters
* Prepending is costlier than appending
* Simple simulation is sufficient here

---

## Problem Difficulty Analysis

This is an **Easy-level** problem.

It focuses on:

* String operations
* Simulation
* Basic logic
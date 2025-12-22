# Watermelon

## Platform
**Codeforces**

## Problem Link
[A. Watermelon](https://codeforces.com/problemset/problem/4/A)

## Problem Statement
One hot summer day, Pete and his friend Billy decided to buy a watermelon. They chose the biggest and the ripest one, in their opinion. After that the watermelon was weighed, and the scales showed `w` kilos.

They have decided to divide the watermelon such that each of the two parts weighs an **even number** of kilos, and there is no leftover. Of course, each part should have weight **at least 1 kilo** (they do not want a degenerate case of one person getting all the watermelon).

Your task is to determine whether it is possible to divide the watermelon as they want.

## Input Format
A single integer `w` (1 ≤ w ≤ 100) — the weight of the watermelon in kilograms.

## Output Format
Print `"YES"` (without quotes) if it is possible to divide the watermelon into two even parts, each weighing at least 1 kilo. Otherwise, print `"NO"`.

## Constraints
- 1 ≤ w ≤ 100

## Example

### Example 1
**Input:** 
```
8
```
**Output:** 
```
YES
```
**Explanation:** 
- Can divide into 2 + 6 = 8 (both even) ✓
- Or 4 + 4 = 8 (both even) ✓

### Example 2
**Input:** 
```
3
```
**Output:** 
```
NO
```
**Explanation:** 
- 3 is odd, cannot be split into two even numbers
- 1 + 2 = 3 (1 is odd) ✗

### Example 3
**Input:** 
```
2
```
**Output:** 
```
NO
```
**Explanation:** 
- 2 = 1 + 1 (both odd) ✗
- Cannot split 2 into two positive even numbers

### Example 4
**Input:** 
```
4
```
**Output:** 
```
YES
```
**Explanation:** 
- 4 = 2 + 2 (both even) ✓

---

## Approach: Mathematical Analysis

## Intuition

For a number to be divisible into two even numbers, we need:
1. The total weight `w` must be **even** (sum of two even numbers is always even)
2. The weight must be **greater than 2** (minimum: 2 + 2 = 4)

**Why w > 2?**
- If w = 2: only split is 1 + 1 (both odd) ✗
- If w = 4: can split as 2 + 2 (both even) ✓
- If w = 6: can split as 2 + 4 or 4 + 2 (both even) ✓

**Mathematical Property**: 
- Any even number ≥ 4 can be expressed as the sum of two positive even numbers
- Formula: `w = 2 + (w - 2)` where both are even if w is even and w > 2

## Algorithm

1. Check if weight is **even**: `w % 2 == 0` or `(w & 1) == 0`
2. Check if weight is **greater than 2**: `w > 2`
3. If both conditions are true → print "YES"
4. Otherwise → print "NO"

## Complexity Analysis

- **Time Complexity**: O(1) — constant time operations (bit check and comparison)
- **Space Complexity**: O(1) — no extra space needed

## Mathematical Proof

**Claim**: An even number w can be divided into two positive even numbers if and only if w > 2.

**Proof**:
- **Necessity (⇒)**: If w can be split into two positive even numbers a and b:
  - a ≥ 2 (minimum even positive number)
  - b ≥ 2 (minimum even positive number)
  - Therefore, w = a + b ≥ 4, so w > 2 ✓

- **Sufficiency (⇐)**: If w > 2 and w is even:
  - Let w = 2k where k ≥ 2 (since w > 2 and even)
  - We can write w = 2 + (2k - 2) = 2 + 2(k - 1)
  - Both 2 and 2(k - 1) are even and positive (since k ≥ 2) ✓

**Conclusion**: The answer is YES if and only if w is even AND w > 2.

## Full Solution

```java
import java.util.*;

public class A_Watermelon {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        // Read the weight of the watermelon
        int weight = sc.nextInt();
        
        // Check two conditions:
        // 1. weight > 2 (cannot divide 2 into two positive even numbers)
        // 2. weight is even (sum of two even numbers is always even)
        
        // Using bitwise AND to check if even: (weight & 1) == 0
        // If last bit is 0, number is even
        if (weight > 2 && (weight & 1) == 0) {
            System.out.println("YES");
        } else {
            System.out.println("NO");
        }
        
        // Close scanner
        sc.close();
    }
}
```

## Alternative Solutions

### Solution 1: Using Modulo Operator
```java
if (weight > 2 && weight % 2 == 0) {
    System.out.println("YES");
} else {
    System.out.println("NO");
}
```
- More readable for beginners
- Equivalent to bitwise AND

### Solution 2: Combined Condition
```java
System.out.println(weight > 2 && weight % 2 == 0 ? "YES" : "NO");
```
- One-liner using ternary operator
- More concise

### Solution 3: Checking Specific Cases
```java
if (weight == 2) {
    System.out.println("NO");
} else if (weight % 2 == 0) {
    System.out.println("YES");
} else {
    System.out.println("NO");
}
```
- More explicit handling of edge cases

## Bitwise vs Modulo

**Bitwise AND (`weight & 1`)**:
```
Examples:
8:  1000 & 1 = 0 (even)
7:  0111 & 1 = 1 (odd)
4:  0100 & 1 = 0 (even)
3:  0011 & 1 = 1 (odd)
```
- Checks the least significant bit
- If LSB = 0 → even, if LSB = 1 → odd
- Slightly faster than modulo (single CPU instruction)

**Modulo Operator (`weight % 2`)**:
- More intuitive and readable
- Equivalent functionality
- Minimal performance difference for small numbers

## Test Cases Analysis

| Input | Even? | > 2? | Output | Explanation |
|-------|-------|------|--------|-------------|
| 1 | No | No | NO | Odd number |
| 2 | Yes | No | NO | Cannot split: 1+1 (both odd) |
| 3 | No | Yes | NO | Odd number |
| 4 | Yes | Yes | YES | 2+2 (both even) ✓ |
| 5 | No | Yes | NO | Odd number |
| 6 | Yes | Yes | YES | 2+4 or 4+2 ✓ |
| 8 | Yes | Yes | YES | 2+6, 4+4, etc. ✓ |
| 100 | Yes | Yes | YES | 2+98, 50+50, etc. ✓ |

## Visual Examples

**Example: w = 8**
```
Possible splits (all valid):
2 + 6 = 8 ✓
4 + 4 = 8 ✓
6 + 2 = 8 ✓
(All parts are even and positive)
```

**Example: w = 2**
```
Only possible split:
1 + 1 = 2 ✗
(Both parts are odd)

Cannot create two even parts!
```

**Example: w = 7**
```
Possible splits:
1 + 6 = 7 (1 is odd) ✗
2 + 5 = 7 (5 is odd) ✗
3 + 4 = 7 (3 is odd) ✗

No way to split into two even parts!
```

## Key Insights

1. **Parity Rule**: Sum of two even numbers is always even
2. **Minimum Case**: The smallest even number ≥ 4 that can be split is 4 (2+2)
3. **Edge Case**: w = 2 is the only even number that cannot be split into two positive even numbers
4. **Bitwise Efficiency**: Using `& 1` is a fast way to check even/odd
5. **Simple Logic**: Problem reduces to two simple conditions

## Common Mistakes to Avoid

1. **Forgetting w = 2 case**: Checking only if even is insufficient
2. **Wrong inequality**: Using `w >= 2` instead of `w > 2`
3. **Not handling odd numbers**: Any odd number is always NO
4. **Overcomplicating**: No need to find actual split, just check if possible
5. **Missing edge cases**: Test with w = 1, 2, 3, 4

## Problem Variations

1. **What if we need three even parts?** → w must be even and w > 4 (minimum: 2+2+2=6)
2. **What if parts can be odd?** → Any w ≥ 2 works (always possible)
3. **What if we want equal parts?** → w must be divisible by 4
4. **What if minimum weight per part is 2?** → Same as current (w > 2 and even)

## Practice Tips

1. **Start simple**: This is problem A, designed to be straightforward
2. **Test edge cases**: Always test w = 1, 2, 3, 4
3. **Understand parity**: Review even/odd arithmetic
4. **Think mathematically**: Reduce to simple conditions
5. **Code clearly**: Readability matters even in simple problems

## Interview Relevance

While this is a beginner problem, it teaches:
- **Edge case analysis**: The w = 2 case is easy to miss
- **Mathematical reasoning**: Proving correctness of simple conditions
- **Bit manipulation**: Using bitwise operations for efficiency
- **Clean code**: Writing clear, concise solutions

---

**Note**: This is Codeforces Problem #4A, one of the earliest and most iconic problems on the platform. It's designed as a warm-up problem to introduce basic input/output and simple conditional logic. Despite its simplicity, many newcomers initially miss the w = 2 edge case, making it a great teaching problem about the importance of thorough testing!
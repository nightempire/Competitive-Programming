# Swap and Delete

## Platform
**HackerEarth**

## Problem Link
[B. Swap and Delete](https://www.hackerearth.com/problem/algorithm/swap-and-delete/)

## Problem Statement
You are given a binary string `s` consisting of characters '0' and '1'. You can perform the following operations on the string:

1. **Swap**: Swap any two characters in the string
2. **Delete**: Delete any character from the string

Your goal is to make the string **bad**. A string is considered **bad** if there exists at least one position `i` where `s[i]` equals the character that should be at position `i` in the inverted string.

More formally, you want to create a string `t` from `s` such that `t[i] ≠ opposite(s[i])` for at least one position `i`, where `opposite('0') = '1'` and `opposite('1') = '0'`.

Find the **minimum number of deletions** required to make the string bad. You can use swaps for free (they don't count toward the answer).

## Input Format
- The first line contains a single integer `t` (1 ≤ t ≤ 1000) — the number of test cases
- For each test case:
  - A single line contains a binary string `s` (1 ≤ |s| ≤ 100,000) consisting of '0' and '1'

## Output Format
For each test case, print a single integer — the minimum number of characters that need to be deleted.

## Constraints
- 1 ≤ t ≤ 1000
- 1 ≤ |s| ≤ 100,000
- String `s` contains only '0' and '1'
- Sum of lengths of all strings across all test cases ≤ 100,000

## Example

### Input
```
4
0011
1010
11010
0
```

### Output
```
0
0
1
1
```

### Explanation

**Test 1**: s = "0011"
- Count of '0's = 2, count of '1's = 2
- We can create string "1100" by swapping
- Original: 0011
- Target:  1100 (inverted)
- All positions match their opposites, so 0 deletions needed
- Answer: **0**

**Test 2**: s = "1010"
- Count of '0's = 2, count of '1's = 2
- We can create string "0101" by swapping
- All positions can match their opposites
- Answer: **0**

**Test 3**: s = "11010"
- Count of '0's = 2, count of '1's = 3
- To create a valid inverted string, we need equal counts
- For position i with '0', we need '1' available (and vice versa)
- After using all available opposites, we have 1 character left
- Answer: **1**

**Test 4**: s = "0"
- Count of '0's = 1, count of '1's = 0
- We need '1' to match with '0', but we don't have any
- Must delete the '0'
- Answer: **1**

## Approach

The solution uses a **greedy matching strategy**:

### Key Insight:
To create a valid inverted string without deletions, for each character in position `i`:
- If `s[i] = '0'`, we need a '1' available (from our pool of swappable characters)
- If `s[i] = '1'`, we need a '0' available (from our pool of swappable characters)

Since we can swap freely, we maintain a frequency count of available '0's and '1's.

### Algorithm:
1. **Count frequencies**: Count the number of '0's and '1's in the string
2. **Match greedily**: Traverse the string from left to right:
   - If current character is '0', try to use a '1' from our pool (decrement count of '1's)
   - If current character is '1', try to use a '0' from our pool (decrement count of '0's)
   - If we can't match (pool is empty), stop matching
3. **Calculate deletions**: The remaining characters in both pools are the ones we couldn't match, so they need to be deleted

### Why does this work?
- Since swaps are free, we can rearrange characters optimally
- We greedily match each character with its opposite as long as opposites are available
- Once we run out of opposites, remaining characters cannot be matched and must be deleted

## Complexity

- **Time Complexity**: O(n) per test case, where n is the length of the string — counting frequencies and single traversal
- **Space Complexity**: O(n) — storing the string and frequency array of size 2
- **Overall**: O(total length of all strings)

## Solution Explanation (Step-by-Step)

1. **Read the number of test cases** `t`
2. **For each test case**:
   - Read the binary string `s`
   - **Count character frequencies**:
     - Create frequency array `freq[2]` where `freq[0]` = count of '0's, `freq[1]` = count of '1's
     - Traverse the string and increment appropriate counters
   - **Greedy matching**:
     - Traverse the string from left to right
     - For each position `i`:
       - If `s[i] = '0'` and we have '1's available (`freq[1] > 0`):
         - Use a '1' to match this '0' (decrement `freq[1]`)
       - Else if `s[i] = '1'` and we have '0's available (`freq[0] > 0`):
         - Use a '0' to match this '1' (decrement `freq[0]`)
       - Else: Cannot match anymore, break the loop
   - **Calculate result**:
     - Sum of remaining frequencies = characters that couldn't be matched
     - Output `freq[0] + freq[1]`
3. **Close the scanner** to prevent resource leaks

## Full Solution

```java
import java.util.Scanner;

public class B_Swap_and_Delete {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        // Read number of test cases
        int t = sc.nextInt();
        
        while (t-- > 0) {
            // Read binary string
            String s = sc.next();
            
            // Count frequency of '0's and '1's
            // freq[0] = count of '0', freq[1] = count of '1'
            int[] freq = new int[2];
            for (char c : s.toCharArray()) {
                if(c == '0') freq[0]++;
                else freq[1]++;
            }
            
            // Greedily match each character with its opposite
            for(int i = 0; i < s.length(); i++) {
                // If current is '0', try to use a '1' to match
                if(s.charAt(i) == '0' && freq[1] > 0) {
                    freq[1]--;
                }
                // If current is '1', try to use a '0' to match
                else if(s.charAt(i) == '1' && freq[0] > 0) {
                    freq[0]--;
                }
                // Can't match anymore, stop
                else break;
            }
            
            // Remaining characters need to be deleted
            System.out.println(freq[0] + freq[1]);
        }
        
        // Close scanner to prevent resource leak
        sc.close();
    }
}
```

## Alternative Explanation

Think of it as a **matching problem**:
- You have a pool of '0's and '1's
- For each position in the original string, you need the opposite character
- Match as many positions as possible using swaps
- Delete the unmatched characters

The answer is simply: `|count(0) - count(1)|`

This is because:
- If counts are equal, all can be matched → 0 deletions
- If counts differ by k, then k characters will be left unmatched → k deletions

## Key Insights

1. **Swap Optimization**: Free swaps mean we can rearrange optimally, so only the counts matter
2. **Greedy Strategy**: Match characters from left to right until we run out of opposites
3. **Simple Formula**: The answer is the absolute difference in character frequencies
4. **Balance Problem**: This is essentially a balancing problem between two character types

## Edge Cases

1. **All same characters**: e.g., "0000" → need to delete all but 0 = 4 deletions (or all)
2. **Single character**: e.g., "0" or "1" → need to delete 1
3. **Equal counts**: e.g., "0011" → 0 deletions
4. **Extreme imbalance**: e.g., "1111110" → delete 5 characters

---

**Note**: This problem demonstrates how free operations (swaps) can simplify a problem to just counting and matching. The greedy approach works because we can rearrange the string optimally before deciding what to delete.
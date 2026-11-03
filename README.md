# Leetcode_Day94
# Day 94 — Longest Palindrome

**LeetCode 409 | Easy | Java**

## Problem

Given a string `s` containing uppercase and lowercase English letters, return the length of the longest palindrome that can be built using those letters.

A palindrome is a string that reads the same forward and backward.

**Example 1:**

Input: `s = "abccccdd"`

Output: `7`

Explanation: One possible palindrome is `"dccaccd"`, with a length of 7.

---

## Approach: Frequency Counting

I used a frequency array to count how many times each character appears in the string.

1. Create an integer array of size 128 to store character frequencies.
2. Traverse the string and increase the frequency of each character.
3. Iterate through the frequency array:
   - If a character appears an even number of times, use all its occurrences.
   - If it appears an odd number of times, use all occurrences except one.
4. Keep track of whether at least one odd frequency exists.
5. If an odd frequency exists, add one extra character to the final length to place it in the middle.

This works because a palindrome needs matching characters on both sides, while only one character can occupy the center.

---

## Java Code

```java
class Solution {
    public int longestPalindrome(String s) {
        int freq[] = new int[128];

        for(char c : s.toCharArray()) {
            freq[c]++;
        }

        int length = 0;
        boolean oddFound = false;

        for(int count : freq) {
            if(count % 2 == 0) {
                length += count;
            } else {
                length += count - 1;
                oddFound = true;
            }
        }

        if(oddFound) {
            length++;
        }

        return length;
    }
}
```

---

## Complexity Analysis

**Time Complexity: O(n)**

- Counting character frequencies takes O(n).
- Traversing the fixed-size frequency array takes O(128), which is constant.

**Space Complexity: O(1)**

The frequency array always has a fixed size of 128, regardless of the input string length.

---

## What I Learned

- How frequency counting can simplify string problems.
- Why even character frequencies can be completely used in a palindrome.
- How odd frequencies contribute all but one occurrence.
- Why only one odd-frequency character can be placed in the center.

## Key Takeaway

Not every character needs to be used to create the longest palindrome.

Sometimes, understanding which elements to keep and which to leave out is the key to finding the best possible answer.

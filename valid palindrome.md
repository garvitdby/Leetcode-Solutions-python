# Intuition
<!-- Describe your first thoughts on how to solve this problem. -->
The core idea is to verify if a string reads the same forwards and backwards, but with a specific constraint: we only consider alphanumeric characters and ignore their case. This naturally suggests a two-pointer approach, starting one pointer at the beginning and one at the end of the string. We then iteratively move these pointers inwards, skipping any non-alphanumeric characters, and comparing the alphanumeric characters in a case-insensitive manner. If at any point the characters don't match, it's not a palindrome. If all valid pairs match, it is a palindrome.

# Approach
<!-- Describe your approach to solving the problem. -->
The solution employs a two-pointer strategy combined with a helper function to identify alphanumeric characters:

**Initialization:**
- Two pointers, l (left) and r (right), are initialized. l points to the beginning of the string (index 0), and r points to the end of the string (index len(s) - 1).
**Main Loop:**
- A while loop continues as long as l < r. This ensures that the pointers have not crossed or met.
**Skipping Non-Alphanumeric Characters:**
- Inside the main loop, nested while loops are used to advance l and r past any non-alphanumeric characters:
- The inner while l < r and not self.alphaNum(s[l]): loop increments l until s[l] is an alphanumeric character. The l < r condition is crucial to prevent l from potentially exceeding r if the entire remaining substring from l onwards consists of non-alphanumeric characters.
- Similarly, the inner while r > l and not self.alphaNum(s[r]): loop decrements r until s[r] is an alphanumeric character. The r > l condition is used to prevent r from potentially going below l.
**Character Comparison:**
- Once both s[l] and s[r] are confirmed to be alphanumeric characters (and l < r still holds after skipping), their lowercase versions are compared: if s[l].lower() != s[r].lower():.
- If the characters do not match, the string is not a palindrome, and the function immediately returns False.
**Advance Pointers:**
- If the characters match, the pointers are moved inwards: l is incremented (l + 1), and r is decremented (r - 1).
**Return True:**
- If the while l < r loop completes without ever finding a mismatch, it means all valid alphanumeric character pairs matched. Therefore, the string is a palindrome, and the function returns True.
**alphaNum Helper Function:**
- This private helper method self.alphaNum(c) checks if a given character c is alphanumeric. It does this by checking the ASCII values [2] of the character:
- Is it an uppercase letter ('A' through 'Z')?
- Is it a lowercase letter ('a' through 'z')?
- Is it a digit ('0' through '9')?
If any of these conditions are true, the character is alphanumeric, and the function returns True; otherwise, it returns False.

# Complexity
- Time complexity:
<!-- Add your time complexity here, e.g. $$O(n)$$ -->
**\(O(N)\),** where N is the length of the string s. In the worst case, both pointers l and r traverse the entire string, examining each character at most a constant number of times (checking if it's alphanumeric and then comparing).

- Space complexity:
<!-- Add your space complexity here, e.g. $$O(n)$$ -->
**\(O(1)\),** The algorithm uses a constant amount of extra space for the two pointers (l and r) and the call stack for the alphaNum helper function. No additional data structures whose size depends on the input string length are used. 

# Code
```python3 []
class Solution:
    def isPalindrome(self, s: str) -> bool:
        l, r = 0, len(s) - 1

        while l < r:
            while l < r and not self.alphaNum(s[l]):
                l += 1
            while r > l and not self.alphaNum(s[r]):
                r -= 1
            if s[l].lower() != s[r].lower():
                return False
            l, r = l + 1, r - 1

        return True

    def alphaNum(self, c):
        return (ord('A') <= ord(c) <= ord('Z') or
        ord('a') <= ord(c) <= ord('z') or
        ord('0') <= ord(c) <= ord('9'))
```

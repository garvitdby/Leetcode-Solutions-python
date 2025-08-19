# Is Subsequence

## Intuition

The core idea is to search for characters of string `s` within string `t` while maintaining their relative order. Finding the characters of `s` in `t` in the correct sequence is sufficient.

## Approach

The solution uses a two-pointer technique:

### Initialization:

*   `i` is initialized to 0, which represents the current character being examined in `s`.
*   `j` is initialized to 0, representing the current character being examined in `t`.

### Iteration:

A `while` loop continues as long as both pointers are within the bounds of their respective strings:

*   **Match:** If `s[i]` matches `t[j]`, the current character of `s` has been found in `t`. Both pointers are incremented to move to the next characters in both strings.
*   **No Match:** If `s[i]` does not match `t[j]`, only the pointer `j` (for string `t`) is incremented. The current character of `s` is being searched for in `t`. If it's not at the current position in `t`, the next character in `t` is checked.

### Result:

After the loop, the solution checks if `i` has reached the end of `s`.

*   If `i == len(s)`, all characters of `s` have been found in `t` in the correct relative order, so `s` is a subsequence of `t`, and the function returns `True`.
*   Otherwise, if `i != len(s)`, some characters of `s` were not found in `t` in the correct order, and the function returns `False`.

## Complexity

*   **Time complexity:** $$O(M)$$, where M is the length of string `t`. The algorithm iterates through all characters of `t` once in the worst-case scenario. The pointer `i` for `s` might also move but will never exceed the length of `s`, which is also bounded by `M`.
*   **Space complexity:** $$O(1)$$. The algorithm only uses a constant amount of extra space for the two pointers `i` and `j`, regardless of the input string sizes.

## Code

```python
class Solution:
    def isSubsequence(self, s: str, t: str) -> bool:
        i, j = 0, 0

        while i < len(s) and j < len(t):
            if s[i] == t[j]:
                i += 1
            j += 1
        return True if i == len(s) else False

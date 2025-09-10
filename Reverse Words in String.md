# Intuition
<!-- Describe your first thoughts on how to solve this problem. -->
The most straightforward way to reverse the order of words in a string is to use the built-in string and list manipulation methods available in Python.
First, we need to handle any leading, trailing, or multiple spaces that might be present in the input string.
Next, we can split the cleaned string into a list of individual words.
Then, we reverse the order of the words in the list.
Finally, we join the words back into a single string with a single space separating them. 
This process can be accomplished efficiently and concisely using Python's strip(), split(), list slicing [::-1], and join() methods.

# Approach
<!-- Describe your approach to solving the problem. -->
1. s = s.strip(): This line uses the strip() method to remove any leading and trailing whitespace from the input string s. This ensures that the final output does not have extra spaces at the beginning or end.
2. words = s.split(): The split() method, when called without an argument, automatically handles multiple spaces between words by treating any sequence of whitespace as a single delimiter. It returns a list of words.
3. reversed_words = words[::-1]: This uses Python's list slicing with a step of -1 ([::-1]) to create a new list with the elements of the words list in reverse order. This is a very clean and Pythonic way to reverse a list.
4. return ' '.join(reversed_words): The join() method concatenates the elements of the reversed_words list into a new string. The string ' ' is used as the separator, which inserts a single space between each word. The final string is then returned.

# Complexity
- Time complexity:
<!-- Add your time complexity here, e.g. $$O(n)$$ -->
**\(O(N)\),** Overall, the dominant operations are linear with respect to the input size. 
- Space complexity:
<!-- Add your space complexity here, e.g. $$O(n)$$ -->
**\(O(N)\),** where N is the length of the input string s
# Code
```python3 []
class Solution:
    def reverseWords(self, s: str) -> str:
        s = s.strip()
        words = s.split()
        reversed_words = words[::-1]
        return ' '.join(reversed_words)
```

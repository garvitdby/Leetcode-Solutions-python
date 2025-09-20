# Intuition
<!-- Describe your first thoughts on how to solve this problem. -->
To form the word "balloon", we need specific counts of each required character: one 'b', one 'a', two 'l's, two 'o's, and one 'n'. The maximum number of "balloon" instances we can create is limited by the character we have the fewest of, relative to its requirement.

For example, if we have 10 'b's, 10 'a's, 10 'l's, 10 'o's, and 10 'n's, we can only form five "balloon" words. This is because we need two 'l's and two 'o's for each word, so the 10 available 'l's and 'o's can only produce \(10//2=5\) instances. The minimum number of instances possible across all required characters is the overall maximum.
 
The approach is to: 
- Count the frequency of each character in the input text.
- Count the frequency of each character in the word "balloon".
- For each unique character in "balloon", calculate how many full "balloon" words can be formed based on the available characters in text.
- The final result is the minimum of these calculated numbers.

# Approach
<!-- Describe your approach to solving the problem. -->
The provided Python code uses collections.Counter to simplify the frequency counting, which is an elegant and efficient way to implement this logic. 
1. **Count frequencies:**
- textCounter = Counter(text): Creates a hashmap (dictionary) textCounter to store the frequency of each character in the input string text.
- word = Counter("balloon"): Creates a hashmap word to store the frequency of each character in the target word "balloon". This will tell us that for each "balloon" word, we need 1 'b', 1 'a', 2 'l's, 2 'o's, and 1 'n'.
2. **Find the limiting character:**
- result = len(text): Initializes result to a value guaranteed to be greater than any possible answer. The length of the text is a safe choice since the number of balloons can never exceed the total number of characters. A better practice might be to initialize it to float('inf').
- for char in word:: The code iterates through the unique characters required for "balloon": 'b', 'a', 'l', 'o', 'n'.
- result = min(result, textCounter[char] // word[char]): For each required character, it calculates the number of times it can form a "balloon" (textCounter[char] // word[char]) and updates result with the minimum value seen so far.
- For 'b', 'a', and 'n', word[char] is 1, so the calculation is textCounter[char] // 1.
- For 'l' and 'o', word[char] is 2, so the calculation is textCounter[char] // 2.
- The use of integer division // correctly handles cases where a character's count is not a multiple of its required count.
3. **Return the minimum:**
- return result: The loop finishes after checking all required characters, and the minimum value stored in result is returned.
 
This approach is correct and effectively finds the bottle-neck character that limits the total number of "balloon" words.

# Complexity
- Time complexity:
<!-- Add your time complexity here, e.g. $$O(n)$$ -->
**\(O(N)\),** where \(N\) is the length of the input string text

- Space complexity:
<!-- Add your space complexity here, e.g. $$O(n)$$ -->
**\(O(1)\)** because the size of these hashmaps is fixed and does not grow with the input size \(N\), the space complexity is constant.

# Code
```python3 []
class Solution:
    def maxNumberOfBalloons(self, text: str) -> int:
        textCounter = Counter(text)
        word = Counter("balloon")

        result = len(text)
        for char in word:
            result = min(result, textCounter[char] // word[char])

        return result
```

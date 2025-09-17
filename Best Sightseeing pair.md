# Intuition
<!-- Describe your first thoughts on how to solve this problem. -->
The problem asks for the maximum value of values[i] + values[j] + i - j for all pairs of indices (i, j) where i < j. 

The expression values[i] + values[j] + i - j can be rewritten as (values[i] + i) + (values[j] - j). This rephrasing simplifies the problem. We can iterate through the array with a single pass, keeping track of the maximum value of values[i] + i encountered so far. As we iterate through the array with a pointer j, we calculate the score using the current values[j] - j and the previously stored maximum values[i] + i. 

# Approach
<!-- Describe your approach to solving the problem. -->
The solution uses a single-pass greedy approach:
1. **Initialization:**
- **max_score:** A variable to store the maximum score found. It is initialized to 0.
- **best:** A variable to store the maximum value of values[i] + i encountered for all i less than the current index j. It is initialized with values[0]. This implicitly sets the initial best value as values[0] + 0.
2. **Iteration:**
- The code iterates through the values array with a single loop, with index j starting from 1.
- **Calculate Potential Score:** In each iteration, the potential score for the current j is calculated as best + values[j] - j. The best variable holds the maximum values[i] + i from all previous indices, ensuring that we consider the best possible i for the current j.
- **Update Maximum Score:** max_score is updated to be the maximum of its current value and the potential score.
- **Update best:** best is updated to the maximum of its current value and values[j] + j. This prepares for the next iteration by considering the current index j as a potential candidate for a future maximum values[i] + i.
3. **Return Value:** After the loop completes, max_score holds the maximum score found across all valid pairs (i, j).

# Complexity
- Time complexity:
<!-- Add your time complexity here, e.g. $$O(n)$$ -->
**\(O(n)\),** where n is the number of elements in the values array. The solution uses a single loop that iterates through the array once.

- Space complexity:
<!-- Add your space complexity here, e.g. $$O(n)$$ -->
**\(O(1)\),** as the solution only uses a few variables to store the intermediate maximums, regardless of the size of the input array.

# Code
```python3 []
class Solution:
    def maxScoreSightseeingPair(self, values: List[int]) -> int:
        max_score = 0
        best = values[0]

        for j in range(1, len(values)):
            max_score = max(max_score, best + values[j] - j)
            best = max(best, values[j] + j)

        return max_score
```

# Intuition
<!-- Describe your first thoughts on how to solve this problem. -->
The code aims to efficiently determine if an increasing triplet subsequence exists within the input array nums. To do this, it maintains two variables: num1, which stores the smallest number encountered so far, and num2, which stores the smallest number that is greater than num1 (representing a potential second element of the triplet). By greedily updating these values, the algorithm maximizes the chances of finding a third number larger than both, thereby indicating an increasing triplet and returning True.

# Approach
<!-- Describe your approach to solving the problem. -->
Uses a single-pass greedy approach that maintains the two smallest numbers encountered to find the target triplet.

# Complexity
- Time complexity:
<!-- Add your time complexity here, e.g. $$O(n)$$ -->
O(N) - The algorithm iterates through the nums array once, performing constant time operations (comparisons and assignments) in each iteration. The time complexity is linear, proportional to the number of elements (N) in the input array.

- Space complexity:
<!-- Add your space complexity here, e.g. $$O(n)$$ -->
O(1) - The algorithm uses only two extra variables, num1 and num2, to store the minimum and second minimum values. The space used is constant, independent of the size of the input array. 

# Code
```python3 []
class Solution:
    def increasingTriplet(self, nums: List[int]) -> bool:
        num1 = num2 = float('inf')
        for num in nums:
            if num <= num1:
                num1 = num
            elif num <= num2:
                num2 = num
            else:
                return True
        return False
```

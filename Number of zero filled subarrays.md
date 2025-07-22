# Intuition
<!-- Describe your first thoughts on how to solve this problem. -->
The code iterates through the nums array to identify contiguous sequences of zeroes. It tracks the current length of the zero sequence in count and adds count to the result for each zero encountered, effectively summing up the number of subarrays ending at the current zero.

# Approach
<!-- Describe your approach to solving the problem. -->
This uses a single pass to count contiguous subarrays of zeroes.

# Complexity
- Time complexity:
<!-- Add your time complexity here, e.g. $$O(n)$$ -->
O(N) - The code scans the nums array once, resulting in linear time complexity relative to the number of elements.

- Space complexity:
<!-- Add your space complexity here, e.g. $$O(n)$$ -->
O(1) - The algorithm uses a constant amount of extra space for the result and count variables, regardless of the size of the input array.

# Code
```python3 []
class Solution:
    def zeroFilledSubarray(self, nums: List[int]) -> int:
        result, count = 0, 0

        for num in nums:
            if num == 0:
                count += 1
                result += count
            else:
                count = 0
        return result
```

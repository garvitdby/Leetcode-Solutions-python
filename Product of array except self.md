# Intuition
<!-- Describe your first thoughts on how to solve this problem. -->
IntuitionTo find the product of all elements except the current one at nums[i], the product of elements to its left and right is needed. The code calculates these two products in separate passes and stores them in the answer array.

# Approach
<!-- Describe your approach to solving the problem. -->
This uses a two-pass scan without extra arrays (optimized prefix/suffix products).

# Complexity
- Time complexity:
<!-- Add your time complexity here, e.g. $$O(n)$$ -->
O(N) - The code scans the array twice, each taking linear time relative to the number of elements (N).

- Space complexity:
<!-- Add your space complexity here, e.g. $$O(n)$$ -->
O(1) (excluding the output array) - The algorithm uses a constant amount of extra space for the prefix and postfix variables, regardless of the input array's size. The output array is part of the required output, not extra space.

# Code
```python3 []
class Solution:
    def productExceptSelf(self, nums: List[int]) -> List[int]:
        answer = [1] * (len(nums))

        prefix = 1
        for i in range(len(nums)):
            answer[i] = prefix
            prefix *= nums[i]

        postfix = 1
        for i in range(len(nums) - 1, -1, -1):
            answer[i] *= postfix
            postfix *= nums[i]

        return answer 
```

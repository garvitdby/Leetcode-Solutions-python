# Intuition
<!-- Describe your first thoughts on how to solve this problem. -->
Consider an array A of size N. We want to right-rotate it by k positions. This means the last k elements should move to the beginning, and the first N-k elements should shift to the right.

# Approach
<!-- Describe your approach to solving the problem. -->
Reverse Array

# Complexity
- Time complexity:
<!-- Add your time complexity here, e.g. $$O(n)$$ -->
O(n), as it performs constant number of array reversal operation

- Space complexity:
<!-- Add your space complexity here, e.g. $$O(n)$$ -->
O(1), as it operates directly on the output array

# Code
```python3 []
class Solution:
    def rotate(self, nums: List[int], k: int) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        n = len(nums)
        k %= n

        def reverse(start, end):
            while start < end:
                nums[start], nums[end] = nums[end], nums[start]
                start += 1
                end -= 1

        reverse(0, n-1)
        reverse(0, k-1)
        reverse(k, n-1)
```

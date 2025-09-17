# Intuition
<!-- Describe your first thoughts on how to solve this problem. -->
The problem is to find the maximum product of a contiguous subarray. A naive approach of checking every subarray would be inefficient. A dynamic programming approach, similar to Kadane's algorithm for maximum subarray sum, can solve this in a single pass. 

The key difference from the sum problem is that a negative number multiplied by a large negative number can result in a large positive number. Therefore, to track the maximum product, we also need to keep track of the minimum product ending at the current position. When we encounter a new number, if it's negative, we swap our current maximum and minimum trackers because multiplying by a negative number will reverse their magnitude.

# Approach
<!-- Describe your approach to solving the problem. -->
The solution implements this dynamic programming strategy.
1. **Initialization:** The algorithm initializes currentmax, currentmin, and globalmax with the first element of the array nums.
- currentmax: Tracks the maximum product of a subarray ending at the current index.
- currentmin: Tracks the minimum product of a subarray ending at the current index.
- globalmax: Stores the overall maximum product found so far.
2. **Iteration:** The code then iterates through the rest of the array, starting from the second element.
3. **Handling Negative Numbers:** For each num, it checks if it is negative. If num is negative, it swaps the values of currentmax and currentmin. This is because multiplying by a negative number will make the previously smallest product the new largest product, and vice versa.
4. **Updating Products:** The currentmax and currentmin are updated for the current position:
- currentmax is set to the maximum of num (starting a new subarray) and num * currentmax (extending the previous maximum subarray).
- currentmin is set to the minimum of num (starting a new subarray) and num * currentmin (extending the previous minimum subarray).
5. **Updating Global Maximum:** After updating currentmax, globalmax is updated to be the maximum of itself and the new currentmax.
6. **Return:** After the loop completes, globalmax holds the maximum product of any contiguous subarray, and this value is returned.

# Complexity
- Time complexity:
<!-- Add your time complexity here, e.g. $$O(n)$$ -->
**\(O(n)\),** where n is the number of elements in nums. The algorithm iterates through the array once.

- Space complexity:
<!-- Add your space complexity here, e.g. $$O(n)$$ -->
**\(O(1)\),** as the algorithm uses a fixed number of variables regardless of the input size.

# Code
```python3 []
class Solution:
    def maxProduct(self, nums: List[int]) -> int:
        currentmax = nums[0]
        currentmin = nums[0]
        globalmax = nums[0]
        for num in nums[1:]:
            if num < 0:
                currentmax, currentmin = currentmin, currentmax

            currentmax = max(num, num * currentmax)
            currentmin = min(num, num * currentmin)

            globalmax = max(globalmax, currentmax)

        return globalmax
```

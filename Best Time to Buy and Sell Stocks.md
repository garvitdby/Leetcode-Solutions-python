# Intuition
<!-- Describe your first thoughts on how to solve this problem. -->
Maintain a running track of the minimum price so far and compute the potential profit for each day by subtracting the current price from this minimum price.

# Approach
<!-- Describe your approach to solving the problem. -->
One Pass

# Complexity
- Time complexity:
<!-- Add your time complexity here, e.g. $$O(n)$$ -->
O(n), as we only traverse through the array once

- Space complexity:
<!-- Add your space complexity here, e.g. $$O(n)$$ -->
O(1), as only constant amount of extra space is used

# Code
```python3 []
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        maxProfit = 0
        minPrice = float('inf')

        for price in prices:
            if price < minPrice:
                minPrice = price 
                
            profit = price - minPrice

            if profit > maxProfit:
                maxProfit = profit
                
        return maxProfit
```

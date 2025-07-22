# Intuition
<!-- Describe your first thoughts on how to solve this problem. -->
The code iterates through the prices array, adding the difference between consecutive prices to the max_profit if the latter is greater than the former. It accumulates profits on every upward price movement effectively simulating buying at the low point and selling at the next high point, thereby maximizing total profit.

# Approach
<!-- Describe your approach to solving the problem. -->
This uses a greedy approach to accumulate profits by adding positive price differences.

# Complexity
- Time complexity:
<!-- Add your time complexity here, e.g. $$O(n)$$ -->
O(N) - The code scans the prices array once, resulting in linear time complexity relative to the number of elements.

- Space complexity:
<!-- Add your space complexity here, e.g. $$O(n)$$ -->
O(1) - The algorithm uses a constant amount of extra space for the max_profit variable, regardless of the size of the input array.

# Code
```python3 []
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        max_profit = 0

        for i in range(1, len(prices)):
            if prices[i] > prices[i - 1]:
                max_profit += prices[i] - prices[i - 1]
        return max_profit
```

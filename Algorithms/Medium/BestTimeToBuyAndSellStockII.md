![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 122. [Best Time To Buy And Sell Stock II](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii)

### Solution :

Method 1 :
```rust
impl Solution {
    pub fn max_profit(prices: Vec<i32>) -> i32 {
        /* Option 1 */
        let mut result: i32 = 0;
        for index in 1..prices.len() {
            if prices[index-1] < prices[index] {
                result += prices[index] - prices[index-1];
            }
        }

        return result
        /* Option 2

        return (1..prices.len()).map(|index| 0.max(prices[index]-prices[index-1])).sum()
        */
    }
}
```

Method 2 (Monotonic Stack) :
```rust
impl Solution {
    pub fn max_profit(prices: Vec<i32>) -> i32 {
        let mut stack: Vec<i32> = vec![];
        let mut result: i32 = 0;
        for price in prices {
            if stack.len() > 0 && *stack.last().unwrap() > price {
                if stack.len() >= 2 {
                    result += stack.last().unwrap() - stack[0];
                }

                stack = vec![];
            }

            if stack.len() == 0 || *stack.last().unwrap() < price {
                stack.push(price);
            }
        }

        if stack.len() >= 2 {
            result += stack.last().unwrap() - stack[0];
        }

        return result
    }
}
```

### Solution :

Method 1 (Monotonic Stack) :
```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        result = 0
        stack = []
        for price in prices:
            if stack and stack[-1] > price:
                if len(stack) >= 2:
                    result += (stack[-1] - stack[0])

                stack = []

            if not stack or stack[-1] < price:
                stack.append(price)

        if stack and len(stack) >= 2:
            result += (stack[-1] - stack[0])

        return result
```

Method 2 (Two Pointers) :
```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        n = len(prices)
        left, right = 0, 1
        result = 0
        while right < n:
            if prices[right-1] > prices[right]:
                result += prices[right-1] - prices[left]
                left = right

            right += 1

        result += prices[right-1] - prices[left]

        return result
```

Method 3 :
```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        # Option 1
        result = 0
        for index in range(1, len(prices)):
            result += max(0, prices[index] - prices[index-1])

        return result
        """
        # Option 2

        return sum([max(0, prices[index] - prices[index-1]) for index in range(1, len(prices))])
        """
```

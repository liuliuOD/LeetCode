![language-RUST](https://img.shields.io/badge/%20-RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 121. [Best Time To Buy And Sell Stock](https://leetcode.com/problems/best-time-to-buy-and-sell-stock)

### Solution :

Method 1 :
```rust
impl Solution {
    pub fn max_profit(prices: Vec<i32>) -> i32 {
        let mut minimum_price: i32 = i32::MAX;
        let mut result: i32 = 0;

        for &current_price in prices.iter() {
            minimum_price = *[minimum_price, current_price].iter().min().unwrap();
            let sold_now_profit: i32 = current_price - minimum_price;
            result = *[result, sold_now_profit].iter().max().unwrap();
        }

        return result
    }
}
```

### Solution :

Method 1 :
```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        result = 0
        minimum_price = float('inf')

        for price in prices:
            minimum_price = min(minimum_price, price)
            sold_now_profit = price - minimum_price
            result = max(result, sold_now_profit)

        return result
```

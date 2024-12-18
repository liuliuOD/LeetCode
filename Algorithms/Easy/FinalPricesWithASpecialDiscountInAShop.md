![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 1475. [Final Prices With A Special Discount In A Shop](https://leetcode.com/problems/final-prices-with-a-special-discount-in-a-shop)

### Solution :

Method 1 (Brute Force, Time Complexity: $O(N^2)$, Space Complexity: $O(1)$ (N: the number of the elements in `prices`)) :
```rust
impl Solution {
    pub fn final_prices(prices: Vec<i32>) -> Vec<i32> {
        let n: usize = prices.len();
        let mut result: Vec<i32> = Vec::new();
        for index in 0..n {
            let price: i32 = prices[index];
            for index_discount in index+1..n {
                if prices[index_discount] <= price {
                    result.push(price - prices[index_discount]);
                    break;
                }
            }

            if result.len() == index {
                result.push(price);
            }
        }

        return result
    }
}
```

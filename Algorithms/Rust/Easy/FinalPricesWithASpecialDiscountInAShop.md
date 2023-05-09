## [Final Prices With A Special Discount In A Shop](https://leetcode.com/problems/final-prices-with-a-special-discount-in-a-shop)

### Solution :

Method 1 (Monotomic Stack) :
```rust
impl Solution {
    pub fn final_prices(prices: Vec<i32>) -> Vec<i32> {
        let mut discounts = vec![];
        let mut stack = vec![];
        for index in (0..prices.len()).rev() {
            while !stack.is_empty() {
                if let Some(&price) = stack.last() {
                    if price <= prices[index] {
                        discounts.push(price);
                        break;
                    }
                    stack.pop();
                }
            }
            if stack.is_empty() {
                discounts.push(0);
            }

            stack.push(prices[index]);
        }
        discounts.reverse();

        prices.iter().zip(discounts).map(|(price, discount)| price - discount).collect()
    }
}
```

Method 2 (Monotonic Stack, without additional subtraction) :
```rust
impl Solution {
    pub fn final_prices(prices: Vec<i32>) -> Vec<i32> {
        let mut ans = vec![];
        let mut stack = vec![];
        for index in (0..prices.len()).rev() {
            let mut discount = 0;
            while !stack.is_empty() {
                if let Some(&price) = stack.last() {
                    if price <= prices[index] {
                        discount = price;
                        break;
                    }
                    stack.pop();
                }
            }
            ans.push(prices[index] - discount);

            stack.push(prices[index]);
        }
        ans.reverse();
        ans
    }
}
```

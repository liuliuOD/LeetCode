![language-RUST](https://img.shields.io/badge/%20-RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 2678. [Number Of Senior Citizens](https://leetcode.com/problems/number-of-senior-citizens)

### Solution :

Method 1 (In biweekly contest 104) :
```rust
impl Solution {
    pub fn count_seniors(details: Vec<String>) -> i32 {
        let mut result = 0;
        for detail in details {
            let mut tt = detail.chars().rev();
            tt.next();
            tt.next();
            if tt.next().unwrap().to_digit(10).unwrap() + 10 * tt.next().unwrap().to_digit(10).unwrap() > 60 {
                result += 1;
            }
        }
        result as i32
    }
}
```

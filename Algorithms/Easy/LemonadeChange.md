![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 860. [Lemonade Change](https://leetcode.com/problems/lexicographically-smallest-string-after-a-swap)

### Solution :

Method 1 (Time Complexity: $O(N)$, Space Complexity: $O(1)$ (N: number of the elements in `bills`)) :
```Rust
impl Solution {
    pub fn lemonade_change(bills: Vec<i32>) -> bool {
        let mut amount_5_dollar: usize = 0;
        let mut amount_10_dollar: usize = 0;
        for bill in bills {
            if bill == 5 {
                amount_5_dollar += 1;
            } else if bill == 10 {
                if amount_5_dollar == 0 {
                    return false
                }

                amount_5_dollar -= 1;
                amount_10_dollar += 1;
            } else if bill == 20 {
                if amount_10_dollar == 0 {
                    if amount_5_dollar < 3 {
                        return false
                    }

                    amount_5_dollar -= 3;
                } else if amount_10_dollar > 0 {
                    if amount_5_dollar == 0 {
                        return false
                    }

                    amount_5_dollar -= 1;
                    amount_10_dollar -= 1;
                }
            }
        }

        return true
    }
}
```

![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 2843. [Count Symmetric Integers](https://leetcode.com/problems/count-symmetric-integers)

### Solution :

Method 1 (Time Complexity: $O((H-L)*D)$, Space Complexity: $O(D)$ (H: the value of `high`, L: the value of `low`, D: the number of digits in `high`)) :
```rust
impl Solution {
    pub fn count_symmetric_integers(low: i32, high: i32) -> i32 {
        let mut result: i32 = 0;
        for num in low..=high {
            let mut number_digit: usize = 0;
            let mut temp: i32 = num;
            while temp > 0 {
                temp /= 10;
                number_digit += 1;
            }

            if number_digit%2 == 1 {
                continue;
            }

            let str_num: String = num.to_string();
            let digits: &[u8] = str_num.as_bytes();
            let n: usize = digits.len();
            let left: i32 = digits[0..n/2].iter().map(|ascii| *ascii as i32).sum();
            let right: i32 = digits[n/2..n].iter().map(|ascii| *ascii as i32).sum();
            if left == right {
                result += 1;
            }
        }

        return result
    }
}
```

![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 1295. [Find Numbers With Even Number Of Digits](https://leetcode.com/problems/find-numbers-with-even-number-of-digits)

### Solution :

Method 1 (Time Complexity: $O(N)$, Space Complexity: $O(1)$ (N: the number of the elements in `nums`)) :
```rust
impl Solution {
    pub fn find_numbers(nums: Vec<i32>) -> i32 {
        let mut result: i32 = 0;
        for mut num in nums {
            let mut number_of_digits: usize = 0;
            while num > 0 {
                number_of_digits += 1;
                num /= 10;
            }

            if number_of_digits%2 == 0 {
                result += 1;
            }
        }

        return result
    }
}
```

![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 1524. [Number Of Sub-Arrays With Odd Sum](https://leetcode.com/problems/number-of-sub-arrays-with-odd-sum)

### Solution :

Method 1 (Prefix Sum, Time Complexity: $O(N)$, Space Complexity: $O(1)$ (N: the number of elements in `arr`)) :
```rust
const MODULO: i64 = 1_000_000_007;

impl Solution {
    pub fn num_of_subarrays(arr: Vec<i32>) -> i32 {
        let mut counter: [i64; 2] = [0; 2];
        counter[0] = 1;
        let mut result: i64 = 0;
        let mut sum: i32 = 0;
        for num in arr {
            sum = (sum + num) & 1;
            result = (result + counter[(sum as usize + 1) & 1]) % MODULO;
            counter[sum as usize & 1] += 1;
        }

        return result as i32
    }
}
```

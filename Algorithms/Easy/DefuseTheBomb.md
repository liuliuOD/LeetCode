![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 1652. [Defuse The Bomb](https://leetcode.com/problems/defuse-the-bomb)

### Solution :

Method 1 (Time Complexity: $O(N*K)$, Space Complexity: $O(1)$ (N: the number of the elements in `code`, K: the value of `k`)) :
```rust
impl Solution {
    pub fn decrypt(code: Vec<i32>, k: i32) -> Vec<i32> {
        let n: usize = code.len();
        let mut result: Vec<i32> = vec![0; n];
        for index in 0..n {
            let mut sum: i32 = 0;
            for offset in 1..=k.abs() {
                if k < 0 {
                    sum += code[(n as i32+(index as i32 -offset)) as usize % n];
                } else {
                    sum += code[(index as i32 +offset) as usize % n];
                }
            }

            result[index] = sum;
        }

        return result
    }
}
```

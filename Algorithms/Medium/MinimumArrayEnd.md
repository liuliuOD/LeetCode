![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 3133. [Minimum Array End](https://leetcode.com/problems/minimum-array-end)

### Solution :

Method 1 (Brute Force, ERROR: "Memory Limit Exceeded", 666/765, Time Complexity: $O(N^2)$, Space Complexity: $O(N)$ (N: the value of `n`)) :
```rust
impl Solution {
    pub fn min_end(n: i32, x: i32) -> i64 {
        let mut result: Vec<i64> = Vec::from([x as i64]);
        let mut bit: u8 = 0;
        while result.len() < n as usize {
            if x as i64 & 1<<bit <= 0 {
                for index in 0..result.len() {
                    result.push(result[index] | 1<<bit);
                }
            }

            bit += 1;
        }

        return result[n as usize - 1]
    }
}
```

Method 2 (Bitwise, Time Complexity: $O(Log(N))$, Space Complexity: $O(1)$ (N: the value of `n`)) :
```rust
impl Solution {
    pub fn min_end(mut n: i32, x: i32) -> i64 {
        let mut result: i64 = x as i64;
        n -= 1;
        let mut mask: i64 = 1;
        while n > 0 {
            if x as i64 & mask <= 0 {
                result |= (n as i64 & 1) * mask;
                n >>= 1;
            }

            mask <<= 1;
        }

        return result
    }
}
```

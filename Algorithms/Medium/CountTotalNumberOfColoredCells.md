![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 2579. [Count Total Number Of Colored Cells](https://leetcode.com/problems/count-total-number-of-colored-cells)

### Solution :

Method 1 (Simulation, Time Complexity: $O(N)$, Space Complexity: $O(1)$ (N: the value of `n`)) :
```rust
impl Solution {
    pub fn colored_cells(n: i32) -> i64 {
        let mut result: i64 = 1;
        for multiply in 1..n as i64 {
            result += 4 * multiply;
        }

        return result
    }
}
```

Method 2 (Mathematics, Time Complexity: $O(1)$, Space Complexity: $O(1)$) :
```rust
impl Solution {
    pub fn colored_cells(n: i32) -> i64 {
        let n: i64 = n as i64;
        return 1 + 4 * (n - 1) * n / 2
    }
}
```

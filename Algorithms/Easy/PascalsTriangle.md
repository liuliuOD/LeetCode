![language-RUST](https://img.shields.io/badge/%20-RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 118. [Pascal's Triangle](https://leetcode.com/problems/pascals-triangle)

### Solution :

Method 1 (Dynamic Programming) :
```rust
impl Solution {
    pub fn generate(num_rows: i32) -> Vec<Vec<i32>> {
        let num_rows: usize = num_rows as usize;
        let mut result: Vec<Vec<i32>> = vec![vec![]; num_rows];

        for row in 0..num_rows {
            for column in 0..row+1 {
                if column == 0 || column == row {
                    result[row].push(1);
                    continue;
                }
                let temp: i32 = result[row-1][column-1] + result[row-1][column];
                result[row].push(temp);
            }
        }
        return result
    }
}
```

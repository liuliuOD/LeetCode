![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## [Matrix Diagonal Sum](https://leetcode.com/problems/find-the-index-of-the-first-occurrence-in-a-string)

### Solution :

Method 1 :
```rust
impl Solution {
    pub fn diagonal_sum(mat: Vec<Vec<i32>>) -> i32 {
        let n = mat.len();
        let mut result = 0;
        let mut secondary_diagonal = n - 1;
        for i in 0..n {
            result += mat[i][i];
            result += mat[i][secondary_diagonal];
            secondary_diagonal -= 1;
        }
        if n % 2 == 1 {
            let center = n / 2;
            result -= mat[center][center];
        }

        result
    }
}
```

Method 2 :
```rust
impl Solution {
    pub fn diagonal_sum(mat: Vec<Vec<i32>>) -> i32 {
        let n = mat.len();
        let mut result = 0;
        for i in 0..n {
            result += mat[i][i] + mat[i][n - i - 1];
        }
        if n % 2 == 1 {
            let center = n / 2;
            result -= mat[center][center];
        }

        result
    }
}
```

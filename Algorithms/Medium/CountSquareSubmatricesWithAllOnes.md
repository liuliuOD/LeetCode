![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 1277. [Count Square Submatrices With All Ones](https://leetcode.com/problems/count-square-submatrices-with-all-ones)

### Solution :

Method 1 (Brute Force, Time Complexity: $O(M*N*Min(M, N)^2)$, Space Complexity: $O(1)$ (M: the number of the elements in `matrix`, N: the number of the elements in `matrix[0]`)) :
```rust
impl Solution {
    pub fn count_squares(matrix: Vec<Vec<i32>>) -> i32 {
        let m: usize = matrix.len();
        let n: usize = matrix[0].len();
        let mut result: i32 = 0;
        for index_m in 0..m {
            for index_n in 0..n {
                for length in 1..=usize::min(m-index_m, n-index_n) {
                    let mut is_all_ones: bool = true;
                    for offset_m in 0..length {
                        if matrix[index_m+offset_m][index_n+length-1] == 0 {
                            is_all_ones = false;
                            break;
                        }
                    }

                    for offset_n in 0..length {
                        if matrix[index_m+length-1][index_n+offset_n] == 0 {
                            is_all_ones = false;
                            break;
                        }
                    }

                    if !is_all_ones {
                        break;
                    }

                    result += 1;
                }
            }
        }

        return result
    }
}
```

![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 2661. [First Completely Painted Row Or Column](https://leetcode.com/problems/first-completely-painted-row-or-column)

### Solution :

Method 1 (Time Complexity: $O(M*N)$, Space Complexity: $O(M*N)$ (M: the number of the elements in `mat`, N: the number of the elements in `mat[0]`)) :
```rust
impl Solution {
    pub fn first_complete_index(arr: Vec<i32>, mat: Vec<Vec<i32>>) -> i32 {
        let m: usize = mat.len();
        let n: usize = mat[0].len();
        let mut mapping: Vec<(usize, usize)> = vec![(0, 0); m*n + 1];
        for (index_m, row) in mat.iter().enumerate() {
            for (index_n, &num) in row.iter().enumerate() {
                mapping[num as usize] = (index_m, index_n);
            }
        }

        let mut counter_row: Vec<i32> = vec![n as i32; m];
        let mut counter_column: Vec<i32> = vec![m as i32; n];
        for (index, &num) in arr.iter().enumerate() {
            let (index_m, index_n) = mapping[num as usize];
            counter_row[index_m] -= 1;
            counter_column[index_n] -= 1;

            if counter_row[index_m] == 0 || counter_column[index_n] == 0 {
                return index as i32
            }
        }

        unreachable!();
    }
}
```

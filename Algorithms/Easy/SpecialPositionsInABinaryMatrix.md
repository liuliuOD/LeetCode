![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1582. [Special Positions In A Binary Matrix](https://leetcode.com/problems/special-positions-in-a-binary-matrix)

### Solution :

Method 1 :
```rust
impl Solution {
    pub fn num_special(mat: Vec<Vec<i32>>) -> i32 {
        let m: usize = mat.len();
        let n: usize = mat[0].len();
        /* Option 1 */
        let mut summarize_m: Vec<i32> = vec![0; m];
        let mut summarize_n: Vec<i32> = vec![0; n];
        for index_m in 0..m {
            for index_n in 0..n {
                if mat[index_m][index_n] == 1 {
                    summarize_m[index_m] += 1;
                    summarize_n[index_n] += 1;
                }
            }
        }
        /* Option 2

        let summarize_m: Vec<i32> = mat.iter().map(|row| row.iter().sum()).collect();
        let summarize_n: Vec<i32> = (0..n).map(|index_n| mat.iter().map(|row| row[index_n]).sum()).collect();
        */

        let mut result: i32 = 0;
        for index_m in 0..m {
            for index_n in 0..n {
                if mat[index_m][index_n] == 1 && summarize_m[index_m] == 1 && summarize_n[index_n] == 1 {
                    result += 1;
                    break;
                }
            }
        }

        return result
    }
}
```

Method 2 :
```rust
```

### Solution :

Method 1 (Time Complexity: $O(M*N)$, Space Complexity: $O(M+N)$) :
```python
class Solution:
    def numSpecial(self, mat: List[List[int]]) -> int:
        m = len(mat)
        n = len(mat[0])
        summarize_m = [sum(row) for row in mat]
        summarize_n = [sum(mat[index_m][index_n] for index_m in range(m)) for index_n in range(n)]
        result = 0
        for index_m in range(m):
            for index_n in range(n):
                if mat[index_m][index_n] == 1 and summarize_m[index_m] == 1 and summarize_n[index_n] == 1:
                    result += 1

        return result
```

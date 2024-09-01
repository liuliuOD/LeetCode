![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2022. [Convert 1D Array Into 2D Array](https://leetcode.com/problems/convert-1d-array-into-2d-array)

### Solution :

Method 1 (Time Complexity: $O(M*N)$, Space Complexity: $O(N)$ (M: value of `m`, N: value of `n`)) :
```rust
impl Solution {
    pub fn construct2_d_array(original: Vec<i32>, m: i32, n: i32) -> Vec<Vec<i32>> {
        let m: usize = m as usize;
        let n: usize = n as usize;
        let p: usize = original.len();
        if m*n != p {
            return Vec::new()
        }

        let mut row: Vec<i32> = Vec::new();
        let mut result: Vec<Vec<i32>> = Vec::new();
        for index in 0..p {
            row.push(original[index]);

            if (index+1)%n == 0 {
                result.push(row);
                row = Vec::new();
            }
        }

        return result
    }
}
```

### Solution :

Method 1 (Time Complexity: $O(M*N)$, Space Complexity: $O(N)$ (M: value of `m`, N: value of `n`)) :
```python
class Solution:
    def construct2DArray(self, original: List[int], m: int, n: int) -> List[List[int]]:
        total = m * n
        if len(original) != total:
            return []

        index = 0
        result = []
        for _ in range(m):
            row = []
            for _ in range(n):
                row.append(original[index])
                index += 1

            result.append(row)

        return result
```

![language-RUST](https://img.shields.io/badge/%20-RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 74. [Search A 2D Matrix](https://leetcode.com/problems/search-a-2d-matrix)

### Solution :

Method 1 (Binary Search, 2D -> 1D) :
```rust
impl Solution {
    pub fn search_matrix(matrix: Vec<Vec<i32>>, target: i32) -> bool {
        let m: usize = matrix.len();
        let n: usize = matrix[0].len();
        let amount: usize = m * n;
        let mut pointer_left: usize = 0;
        let mut pointer_right: usize = amount - 1;

        while pointer_left <= pointer_right && pointer_right < amount {
            let middle: usize = pointer_left + (pointer_right - pointer_left)/2;
            let point: i32 = matrix[middle/n][middle%n];

            if point == target {
                return true
            }
            else if point > target {
                pointer_right = middle - 1;
            }
            else if point < target {
                pointer_left = middle + 1;
            }
        }

        return false
    }
}
```

### Solution :

Method 1 (Brute Force) :
```python
class Solution:
    def searchMatrix(self, matrix: List[List[int]], target: int) -> bool:
        for m in range(len(matrix)):
            for n in range(len(matrix[m])):
                if matrix[m][n] == target:
                    return True

        return False
```

Method 2 (Binary Search, 2D) :
```python
class Solution:
    def searchMatrix(self, matrix: List[List[int]], target: int) -> bool:
        m = len(matrix)
        n = len(matrix[0])

        pointer_m_left = pointer_n_left = 0
        pointer_m_right, pointer_n_right = m-1, n-1

        while pointer_m_left <= pointer_m_right:
            middle = pointer_m_left + (pointer_m_right-pointer_m_left) // 2

            if matrix[middle][0] == target:
                return True
            elif matrix[middle][0] > target:
                pointer_m_right = middle - 1
            elif matrix[middle][0] < target:
                pointer_m_left = middle + 1

        while pointer_n_left <= pointer_n_right:
            middle = pointer_n_left + (pointer_n_right-pointer_n_left) // 2

            if matrix[pointer_m_right][middle] == target:
                return True
            elif matrix[pointer_m_right][middle] > target:
                pointer_n_right = middle - 1
            elif matrix[pointer_m_right][middle] < target:
                pointer_n_left = middle + 1

        return False
```

Method 3 (Binary Search, 2D -> 1D) :
```python
class Solution:
    def searchMatrix(self, matrix: List[List[int]], target: int) -> bool:
        m = len(matrix)
        n = len(matrix[0])

        pointer_left = 0
        pointer_right = m * n - 1

        while pointer_left <= pointer_right:
            middle = pointer_left + (pointer_right-pointer_left) // 2

            point = matrix[middle//n][middle%n]
            if point == target:
                return True
            elif point > target:
                pointer_right = middle - 1
            elif point < target:
                pointer_left = middle + 1

        return False
```

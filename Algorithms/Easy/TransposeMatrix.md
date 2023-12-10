![language-RUST](https://img.shields.io/badge/%20-RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 867. [Transpose Matrix](https://leetcode.com/problems/transpose-matrix)

### Solution :

Method 1 :
```rust
impl Solution {
    pub fn transpose(matrix: Vec<Vec<i32>>) -> Vec<Vec<i32>> {
        return (0..matrix[0].len()).map(|n| {
            return (0..matrix.len()).map(|m| matrix[m][n]).collect()
        }).collect()
    }
}
```

### Solution :

Method 1 (Time Complexity: $O(M*N)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def transpose(self, matrix: List[List[int]]) -> List[List[int]]:
        m = len(matrix)
        n = len(matrix[0])
        result = [[] for _ in range(n)]
        for index_m in range(m):
            for index_n in range(n):
                result[index_n].append(matrix[index_m][index_n])

        return result
```

Method 2 :
```python
class Solution:
    def transpose(self, matrix: List[List[int]]) -> List[List[int]]:
        # Option 1
        return zip(*matrix)
        """
        # Option 2

        return list(map(list, zip(*matrix)))
        """
```

Method 3 :
```python
class Solution:
    def transpose(self, matrix: List[List[int]]) -> List[List[int]]:
        return map(lambda n: map(lambda m: matrix[m][n], range(len(matrix))), range(len(matrix[0])))
```

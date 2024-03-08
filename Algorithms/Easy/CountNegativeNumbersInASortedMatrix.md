![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1351. [Count Negative Numbers in a Sorted Matrix](https://leetcode.com/problems/count-negative-numbers-in-a-sorted-matrix)

### Solution :

Method 1 :
```rust
impl Solution {
    pub fn count_negatives(grid: Vec<Vec<i32>>) -> i32 {
        let mut result = 0;
        let x = grid.len();
        let y = grid[0].len();
        let mut i = x - 1;
        let mut j = 0;
        while i >= 0 && i < x && j>= 0 && j < y {
            if grid[i][j] < 0 {
                result += y - j;
                i -= 1;
                continue;
            }

            j += 1;
        }

        return result as i32
    }
}
```

### Solution :

Method 1 (Time Complexity: $O(N^2)$) :
```python
class Solution:
    def countNegatives(self, grid: List[List[int]]) -> int:
        result = 0
        for i in range(len(grid)):
            for j in range(len(grid[0])):
                if grid[i][j] >= 0:
                    continue
                result += 1
        return result
```

Method 2 (Time Complexity: $O(I+J)$) :
```python
class Solution:
    def countNegatives(self, grid: List[List[int]]) -> int:
        result = 0
        x = len(grid)
        y = len(grid[0])
        i = x - 1
        j = 0
        while i >= 0 and i < x and j >= 0 and j < y:
            if grid[i][j] >= 0:
                j += 1
            else:
                result += y - j
                i -= 1
        return result
```

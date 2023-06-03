![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2711. [Difference Of Number Of Distinct Values On Diagonals](https://leetcode.com/problems/maximum-strength-of-a-group)

### Solution :

Method 1 (In weekly contest 347) :
```python
class Solution:
    def differenceOfDistinctValues(self, grid: List[List[int]]) -> List[List[int]]:
        self.grid = grid
        result = [[0] * len(grid[0]) for _ in range(len(grid))]
        for i in range(len(self.grid)):
            for j in range(len(self.grid[0])):
                self.left_top = set()
                self.right_bottom = set()
                self.findLeftTop(i-1, j-1)
                self.findRightBottom(i+1, j+1)
                result[i][j] = abs(len(self.left_top) - len(self.right_bottom))
        return result
                
    def findLeftTop(self, i, j):
        if i < 0 or j < 0 or i >= len(self.grid) or j >= len(self.grid[0]):
            return None
        
        self.left_top.add(self.grid[i][j])
        self.findLeftTop(i-1, j-1)

    def findRightBottom(self, i, j):
        if i < 0 or j < 0 or i >= len(self.grid) or j >= len(self.grid[0]):
            return None
        
        self.right_bottom.add(self.grid[i][j])
        self.findRightBottom(i+1, j+1)
```

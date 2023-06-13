![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2352. [Equal Row And Column Pairs](https://leetcode.com/problems/equal-row-and-column-pairs)

### Solution :

Method 1 (Brute Force) :
```python
class Solution:
    def equalPairs(self, grid: List[List[int]]) -> int:
        result = 0
        for i in range(len(grid)):
            for j in range(len(grid[0])):
                n = len(grid)
                isSame = True
                while n > 0:
                    n -= 1
                    if grid[i][n] == grid[n][j]:
                        continue
                    isSame = False
                if isSame:
                    result += 1
        return result
```

Method 2 (Hash List) :
```python
class Solution:
    def equalPairs(self, grid: List[List[int]]) -> int:
        hash_columns = defaultdict(int)
        for j in range(len(grid[0])):
            row = 0
            column_items = list()
            while row < len(grid):
                column_items.append(grid[row][j])
                row += 1
            hash_columns[self.listToHash(column_items)] += 1
        
        result = 0
        for i in range(len(grid)):
            hash_row = self.listToHash(grid[i])
            if hash_row in hash_columns:
                result += hash_columns[hash_row]
        return result

    def listToHash(self, items: List[int]) -> str:
        return hash(','.join(map(str, items)))
```

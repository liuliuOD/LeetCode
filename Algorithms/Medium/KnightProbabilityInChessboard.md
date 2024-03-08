![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 688. [Knight Probability In Chessboard](https://leetcode.com/problems/knight-probability-in-chessboard)

### Solution :

Method 1 (ERROR: "Time Limit Exceeded", 11/22) :
```python
class Solution:
    def knightProbability(self, n: int, k: int, row: int, column: int) -> float:
        if k == 0:
            return 1.0

        return self.moving(n, k, row, column) / (8**k)
    
    def moving(self, n: int, k: int, row: int, column: int) -> int:
        if row < 0 or column < 0 or row >= n or column >= n:
            return 0

        if k == 0:
            return 1

        move_amount = 0
        for move_x, move_y in [(1, 2), (2, 1), (-1, 2), (-2, 1), (1, -2), (2, -1), (-1, -2), (-2, -1)]:
            move_amount += self.moving(n, k-1, row+move_x, column+move_y)
        return move_amount
```

Method 2 (DFS + Memoization) :
```python
class Solution:
    def knightProbability(self, n: int, k: int, row: int, column: int) -> float:
        if k == 0:
            return 1.0

        memoization = defaultdict(int)
        return self.dfs(n, k, row, column, memoization) / (8**k)
    
    def dfs(self, n: int, k: int, row: int, column: int, memoization: Dict[str, int]) -> int:
        if row < 0 or column < 0 or row >= n or column >= n:
            return 0

        if k == 0:
            return 1

        dictKey = self.getDictKey(row, column, k)
        if dictKey in memoization:
            return memoization[dictKey]

        move_amount = 0
        for move_x, move_y in [(1, 2), (2, 1), (-1, 2), (-2, 1), (1, -2), (2, -1), (-1, -2), (-2, -1)]:
            move_amount += self.dfs(n, k-1, row+move_x, column+move_y, memoization)

        memoization[dictKey] = move_amount
        return memoization[dictKey]
    
    def getDictKey(self, row: int, column: int, k: int) -> str:
        return f'{row}-{column}-{k}'
```

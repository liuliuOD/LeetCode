![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2850. [Minimum Moves To Spread Stones Over Grid](https://leetcode.com/problems/minimum-moves-to-spread-stones-over-grid)

### Solution :

Method 1 (Permutation + Choose Minimum) :
```python
class Solution:
    def minimumMoves(self, grid: List[List[int]]) -> int:
        grids_zero = []
        grids_multiple = []
        for index_x in range(3):
            for index_y in range(3):
                amount_stone = grid[index_x][index_y]
                position = (index_x, index_y)
                if amount_stone == 1:
                    continue

                if amount_stone == 0:
                    grids_zero.append(position)
                elif amount_stone > 1:
                    grids_multiple.extend([position] * (amount_stone-1))

        permutations_list = [list(zip(grids_zero, permutation)) for permutation in permutations(grids_multiple)]

        result = float('inf')
        for permutation in permutations_list:
            temp = 0
            for (grid_zero_x, grid_zero_y), (grid_multiple_x, grid_multiple_y) in permutation:
                temp += abs(grid_zero_x-grid_multiple_x) + abs(grid_zero_y-grid_multiple_y)
            result = min(result, temp)

        return result
```

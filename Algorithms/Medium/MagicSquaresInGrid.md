![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 840. [Magic Squares In Grid](https://leetcode.com/problems/magic-squares-in-grid)

### Solution :

Method 1 (Brute Force, Time Complexity: $O(M*N)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def numMagicSquaresInside(self, grid: List[List[int]]) -> int:
        result = 0
        for index_m in range(len(grid)):
            for index_n in range(len(grid[0])):
                result += int(self.is_magic_square(index_m, index_n, grid))

        return result

    def is_magic_square(self, index_m: int, index_n: int, grid: list[list[int]]) -> bool:
        m = len(grid)
        n = len(grid[0])
        if index_m > m-3 or index_n > n-3:
            return False

        visited: set[int] = set()
        sum_vertical = [0] * 3
        sum_horizontal = [0] * 3
        sum_diagonal = [0] * 2
        diagonal_left, diagonal_right = 0, 2
        for offset_m in range(3):
            index_m_next = index_m + offset_m
            for offset_n in range(3):
                index_n_next = index_n + offset_n
                value = grid[index_m_next][index_n_next]
                if value in visited or value < 1 or value > 9:
                    return False
                visited.add(value)

                sum_horizontal[offset_n] += value
                sum_vertical[offset_m] += value
                if diagonal_left == offset_n:
                    sum_diagonal[0] += value
                if diagonal_right + offset_n == 2:
                    sum_diagonal[1] += value

            diagonal_left += 1
            diagonal_right -= 1

        return sum_horizontal[0] <= 15 and len(set(sum_horizontal)) == 1 and len(set(sum_vertical)) == 1 and len(set(sum_diagonal)) == 1 and sum_horizontal[0] == sum_vertical[0] == sum_diagonal[0]
```

![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1970. [Last Day Where You Can Still Cross](https://leetcode.com/problems/last-day-where-you-can-still-cross)

### Solution :

Method 1 (BFS, ERROR: "Time Limit Exceeded" in 3x3 grids) :
```python
class Solution:
    def latestDayToCross(self, row: int, col: int, cells: List[List[int]]) -> int:
        self.grid = [[0]*col for _ in range(row)]
        for index_cell, (num_cell_x, num_cell_y) in enumerate(cells):
            self.grid[num_cell_x-1][num_cell_y-1] = 1

            self.isFind = False
            for index_top in range(col):
                if self.isFind:
                    break
                self.canFromTopToBottom(0, index_top)
            if self.isFind:
                continue

            return index_cell
        return len(cells)

    def canFromTopToBottom(self, index_row: int, index_top: int) -> bool:
        queue = deque([(index_row, index_top)])
        while queue:
            index_row, index_top = queue.popleft()
            if index_row < 0 or index_row >= len(self.grid) or index_top < 0 or index_top >= len(self.grid[0]) or self.grid[index_row][index_top] == 1:
                continue

            if self.isFind:
                return True
            self.isFind = index_row == (len(self.grid) - 1)

            for offset_x, offset_y in [(0, 1), (0, -1), (1, 0), (-1, 0)]:
                index_next_x = index_row + offset_x
                index_next_y = index_top + offset_y
                queue.append((index_next_x, index_next_y))

        return False
```

Method 2 (BFS + Pruning, ERROR: "Time Limit Exceeded" in 37x270 grids) :
```python
class Solution:
    def latestDayToCross(self, row: int, col: int, cells: List[List[int]]) -> int:
        for index_cell in range(len(cells)):
            self.grid = [[0]*col for _ in range(row)]
            for num_cell_x, num_cell_y in cells[:index_cell+1]:
                self.grid[num_cell_x-1][num_cell_y-1] = 1

            if self.canFromTopToBottom():
                continue

            return index_cell
        return len(cells)

    def canFromTopToBottom(self) -> bool:
        queue = deque([])
        for index_y in range(len(self.grid[0])):
            queue.append((0, index_y))

        while queue:
            index_x, index_y = queue.popleft()
            if index_x < 0 or index_x >= len(self.grid) or index_y < 0 or index_y >= len(self.grid[0]) or self.grid[index_x][index_y] == 1:
                continue
            self.grid[index_x][index_y] = 1

            if index_x == (len(self.grid) - 1):
                return True

            for offset_x, offset_y in [(0, 1), (0, -1), (1, 0), (-1, 0)]:
                index_next_x = index_x + offset_x
                index_next_y = index_y + offset_y
                queue.append((index_next_x, index_next_y))

        return False
```

Method 3 (BFS + Binary Search) :
```python
class Solution:
    def latestDayToCross(self, row: int, col: int, cells: List[List[int]]) -> int:
        pointer_left = 0
        pointer_right = len(cells)
        while pointer_left < pointer_right:
            index_cell = pointer_left + (pointer_right - pointer_left) // 2
            self.grid = [[0]*col for _ in range(row)]
            for num_cell_x, num_cell_y in cells[:index_cell+1]:
                self.grid[num_cell_x-1][num_cell_y-1] = 1

            if self.canFromTopToBottom():
                pointer_left = index_cell + 1
            else:
                pointer_right = index_cell
            
        return pointer_right

    def canFromTopToBottom(self) -> bool:
        queue = deque([])
        for index_y in range(len(self.grid[0])):
            queue.append((0, index_y))

        while queue:
            index_x, index_y = queue.popleft()
            if index_x < 0 or index_x >= len(self.grid) or index_y < 0 or index_y >= len(self.grid[0]) or self.grid[index_x][index_y] == 1:
                continue
            self.grid[index_x][index_y] = 1

            if index_x == (len(self.grid) - 1):
                return True

            for offset_x, offset_y in [(0, 1), (0, -1), (1, 0), (-1, 0)]:
                index_next_x = index_x + offset_x
                index_next_y = index_y + offset_y
                queue.append((index_next_x, index_next_y))

        return False
```

Method 4 (DSU) :
```python
class DSU:
    def __init__(self, items_amount: int):
        self.items = list(range(items_amount))

    def find(self, index: int) -> int:
        if self.items[index] != index:
            self.items[index] = self.find(self.items[index])
        return self.items[index]

    def union(self, index_a: int, index_b: int):
        root_a = self.find(index_a)
        root_b = self.find(index_b)
        self.items[root_a] = root_b

class Solution:
    def latestDayToCross(self, row: int, col: int, cells: List[List[int]]) -> int:
        self.col = col
        dsu = DSU(row*col + 2)
        grid = [[1]*col for _ in range(row)]

        for index in reversed(range(len(cells))):
            cell_x, cell_y = cells[index]
            index_cell_x, index_cell_y = cell_x - 1, cell_y - 1
            index_dsu_current = self.DSUIndex(index_cell_x, index_cell_y)

            grid[index_cell_x][index_cell_y] = 0
            # Top
            if index_cell_x == 0:
                dsu.union(0, index_dsu_current)
            # Bottom
            if index_cell_x == row - 1:
                dsu.union(row*col + 1, index_dsu_current)

            for offset_x, offset_y in [(0, 1), (0, -1), (1, 0), (-1, 0)]:
                index_next_x = index_cell_x + offset_x
                index_next_y = index_cell_y + offset_y
                index_dsu_next = self.DSUIndex(index_next_x, index_next_y)
                if index_next_x < 0 or index_next_x >= row or index_next_y < 0 or index_next_y >= col or grid[index_next_x][index_next_y] == 1:
                    continue

                dsu.union(index_dsu_next, index_dsu_current)

            if dsu.find(0) == dsu.find(row*col + 1):
                return index
        return 0

    """
    0: Top
    row*col + 1: Bottom
    x*col + y + 1: order items from 1 to row*col, by top to bottom and left to right
    """
    def DSUIndex(self, index_x: int, index_y: int) -> int:
        return index_x*self.col + (index_y + 1)
```

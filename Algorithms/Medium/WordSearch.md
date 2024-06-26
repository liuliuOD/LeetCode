![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
![language-PHP](https://img.shields.io/badge/PHP-acb1f9?style=for-the-badge&logo=PHP)
---

## 79. [Word Search](https://leetcode.com/problems/word-search)

### Solution :

Method 1 (DFS, ERROR: "Time Limit Exceeded", 84/86) :
```python
class Solution:
    def exist(self, board: List[List[str]], word: str) -> bool:
        for index_row in range(len(board)):
            for index_column in range(len(board[0])):
                if self.dfs((index_row, index_column), 0, set(), word, board):
                    return True
        return False

    def dfs(self, position: Tuple[int], index: int, visited: Set[Tuple[int]], word: str, board: List[List[str]]) -> bool:
        if position in visited:
            return False
        visited.add(position)

        x, y = position[0], position[1]
        if board[x][y] != word[index]:
            return False
        # board[x][y] == word[index] && index is the latest position of word
        if index == len(word)-1:
            return True

        for offset_x, offset_y in [[-1, 0], [0, -1], [0, 1], [1, 0]]:
            x_next = x + offset_x
            y_next = y + offset_y
            if x_next < 0 or x_next >= len(board) or y_next < 0 or y_next >= len(board[0]):
                continue

            if self.dfs((x_next, y_next), index+1, visited.copy(), word, board):
                return True
        return False
```

Method 2 (DFS + Pruning) :
```python
class Solution:
    def exist(self, board: List[List[str]], word: str) -> bool:
        candidates = []
        targets = defaultdict(int)
        for char in word:
            targets[char] += 1

        for index_row in range(len(board)):
            for index_column in range(len(board[0])):
                current = board[index_row][index_column]
                if current in targets:
                    targets[current] -= 1

                if current == word[0]:
                    candidates.append((index_row, index_column))

        for amount_remain in targets.values():
            if amount_remain > 0:
                return False

        for position in candidates:
            if self.dfs(position, 0, set(), word, board):
                return True
        return False

    def dfs(self, position: Tuple[int], index: int, visited: Set[Tuple[int]], word: str, board: List[List[str]]) -> bool:
        if position in visited:
            return False
        visited.add(position)

        x, y = position[0], position[1]
        if board[x][y] != word[index]:
            return False
        if index == len(word)-1:
            return True

        for offset_x, offset_y in [[-1, 0], [0, -1], [0, 1], [1, 0]]:
            x_next = x + offset_x
            y_next = y + offset_y
            if x_next < 0 or x_next >= len(board) or y_next < 0 or y_next >= len(board[0]):
                continue

            if self.dfs((x_next, y_next), index+1, visited.copy(), word, board):
                return True
        return False
```

Method 3 (DFS + Without Visited Set) :
```python
class Solution:
    def exist(self, board: List[List[str]], word: str) -> bool:
        candidates = []
        targets = defaultdict(int)
        for char in word:
            targets[char] += 1

        for index_row in range(len(board)):
            for index_column in range(len(board[0])):
                current = board[index_row][index_column]
                if current in targets:
                    targets[current] -= 1

                if current == word[0]:
                    candidates.append((index_row, index_column))

        for amount_remain in targets.values():
            if amount_remain > 0:
                return False

        for position in candidates:
            if self.dfs(position, 0, word, board):
                return True
        return False

    def dfs(self, position: Tuple[int], index: int, word: str, board: List[List[str]]) -> bool:
        x, y = position[0], position[1]
        if x < 0 or x >= len(board) or y < 0 or y >= len(board[0]):
            return False

        if board[x][y] != word[index]:
            return False
        if index == len(word)-1:
            return True

        temp , board[x][y] = board[x][y], -1
        for offset_x, offset_y in [[-1, 0], [0, -1], [0, 1], [1, 0]]:
            if self.dfs((x+offset_x, y+offset_y), index+1, word, board):
                return True
        board[x][y] = temp
        return False
```

Method 4 (DFS + Backtracking) :
```python
class Solution:
    def exist(self, board: List[List[str]], word: str) -> bool:
        m = len(board)
        n = len(board[0])
        for index_m in range(m):
            for index_n in range(n):
                temp = board[index_m][index_n]
                if temp != word[0]:
                    continue

                board[index_m][index_n] = None
                if self.valid(index_m, index_n, word[1:], board):
                    return True
                board[index_m][index_n] = temp

        return False

    def valid(self, index_m: int, index_n: int, word: str, board: List[List[str]]) -> bool:
        if word == "":
            return True

        m = len(board)
        n = len(board[0])
        # Option 1
        if index_m > 0:
            temp = board[index_m-1][index_n]
            if temp == word[0]:
                board[index_m-1][index_n] = None
                if self.valid(index_m-1, index_n, word[1:], board):
                    return True
                board[index_m-1][index_n] = temp
        if index_m < m-1:
            temp = board[index_m+1][index_n]
            if temp == word[0]:
                board[index_m+1][index_n] = None
                if self.valid(index_m+1, index_n, word[1:], board):
                    return True
                board[index_m+1][index_n] = temp
        if index_n > 0:
            temp = board[index_m][index_n-1]
            if temp == word[0]:
                board[index_m][index_n-1] = None
                if self.valid(index_m, index_n-1, word[1:], board):
                    return True
                board[index_m][index_n-1] = temp
        if index_n < n-1:
            temp = board[index_m][index_n+1]
            if temp == word[0]:
                board[index_m][index_n+1] = None
                if self.valid(index_m, index_n+1, word[1:], board):
                    return True
                board[index_m][index_n+1] = temp
        """
        # Option 2

        for offset_m, offset_n in [(-1, 0), (1, 0), (0, -1), (0, 1)]:
            index_m_next = index_m + offset_m
            index_n_next = index_n + offset_n
            if index_m_next < 0 or index_m_next >= m:
                continue
            if index_n_next < 0 or index_n_next >= n:
                continue

            temp = board[index_m_next][index_n_next]
            if temp != word[0]:
                continue

            board[index_m_next][index_n_next] = None
            if self.valid(index_m_next, index_n_next, word[1:], board):
                return True
            board[index_m_next][index_n_next] = temp
        """

        return False
```

Method 5 (DFS + Backtracking) :
```python
class Solution:
    def exist(self, board: List[List[str]], word: str) -> bool:
        m = len(board)
        n = len(board[0])
        for index_m in range(m):
            for index_n in range(n):
                if self.valid(index_m, index_n, word, board):
                    return True

        return False

    def valid(self, index_m: int, index_n: int, word: str, board: List[List[str]]) -> bool:
        if word == "":
            return True

        if board[index_m][index_n] != word[0]:
            return False
        if len(word) == 1:
            return True

        temp = board[index_m][index_n]
        board[index_m][index_n] = None

        m = len(board)
        n = len(board[0])
        for offset_m, offset_n in [(-1, 0), (1, 0), (0, -1), (0, 1)]:
            index_m_next = index_m + offset_m
            index_n_next = index_n + offset_n
            if index_m_next < 0 or index_m_next >= m:
                continue
            if index_n_next < 0 or index_n_next >= n:
                continue

            if self.valid(index_m_next, index_n_next, word[1:], board):
                return True

        board[index_m][index_n] = temp

        return False
```

### Solution :

Method 1 (DFS) :
```php
class Solution {

    /**
     * @param String[][] $board
     * @param String $word
     * @return Boolean
     */
    function exist($board, $word) {
        $targets = [];
        foreach(str_split($word) as $char) {
            isset($targets[$char])
                ? $targets[$char]++
                : $targets[$char] = 1;
        }

        $positions = [];
        $target = $word[0];
        foreach($board as $indexRow => $row) {
            foreach($row as $indexColumn => $current) {
                if ($current == $target) {
                    $positions[] = [$indexRow, $indexColumn];
                }
                if (isset($targets[$current])) {
                    $targets[$current]--;
                }
            }
        }

        foreach($targets as $amountRemain) {
            if ($amountRemain > 0) {
                return false;
            }
        }

        foreach($positions as $position) {
            if ($this->dfs($position, 0, $word, $board)) {
                return true;
            }
        }

        return false;
    }

    function dfs($position, $index, $word, $board) : bool {
        list($x, $y) = $position;
        if ($x < 0 || $x >= count($board) || $y < 0 || $y >= count($board[0])) {
            return false;
        }

        if ($word[$index] != $board[$x][$y]) {
            return false;
        } else if ($index == strlen($word)-1) {
            return true;
        }

        $temp = $board[$x][$y];
        $board[$x][$y] = -1;
        foreach([[$x-1, $y], [$x, $y-1], [$x, $y+1], [$x+1, $y]] as $positionNext) {
            if ($this->dfs($positionNext, $index+1, $word, $board)) {
                return true;
            }
        }
        $board[$x][$y] = $temp;
        return false;
    }
}
```

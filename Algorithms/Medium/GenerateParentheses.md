![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 22. [Generate Parentheses](https://leetcode.com/problems/generate-parentheses)

### Solution :

Method 1 (Backtracking) :
```python
class Solution:
    def generateParenthesis(self, n: int) -> List[str]:
        self.string = ''
        self.result = []
        self.backtracking('(', 1, 0, n)

        return self.result

    def backtracking(self, symbol: str, amount_left: int, amount_right: int, n: int):
        if amount_left == amount_right and amount_left == n:
            self.result.append(self.string+symbol)
            return None

        self.string += symbol
        if amount_left < n:
            self.backtracking('(', amount_left+1, amount_right, n)
        if amount_left > amount_right:
            self.backtracking(')', amount_left, amount_right+1, n)

        self.string = self.string[:-1]
```

Method 2 (Backtracking + Enum) :
```python
from enum import Enum
class Parenthesis(Enum):
    LEFT = '('
    RIGHT = ')'

class Solution:
    def generateParenthesis(self, n: int) -> List[str]:
        self.string = ''
        self.result = []
        self.backtracking(Parenthesis.LEFT.value, 1, 0, n)

        return self.result
    
    def backtracking(self, symbol: str, amount_left: int, amount_right: int, n: int):
        if amount_left == amount_right and amount_left == n:
            self.result.append(self.string+symbol)
            return None
        
        self.string += symbol
        if amount_left < n:
            self.backtracking(Parenthesis.LEFT.value, amount_left+1, amount_right, n)
        if amount_left > amount_right:
            self.backtracking(Parenthesis.RIGHT.value, amount_left, amount_right+1, n)
        
        self.string = self.string[:-1]
```

![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2698. [Find The Punishment Number Of An Integer](https://leetcode.com/problems/find-the-punishment-number-of-an-integer)

### Solution :

Method 1 (In weekly contest 346, DFS) :
```python
class Solution:
    def punishmentNumber(self, n: int) -> int:
        result = 0
        for i in range(1, n+1):
            result += self.findNumber(i)
            
        return result

    def findNumber(self, i: int) -> int:
        power = i*i
        if self.valid(i, str(power)):
            return power
        return 0
    
    def valid(self, target: int, power: str) -> bool:
        for i in range(1, len(power)+1):
            if self.dfs(int(power[:i]), target, power[i:]):
                return True
        return False
    
    def dfs(self, value: int, target: int, s: str) -> bool:
        if len(s) == 0:
            return value == target
        if value + int(s) == target:
            return True
        for i in range(1, len(s)+1):
            if self.dfs(value+int(s[:i]), target, s[i:]):
                return True
        
        return False
```

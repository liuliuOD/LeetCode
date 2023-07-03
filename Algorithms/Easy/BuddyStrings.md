![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 859. [Buddy Strings](https://leetcode.com/problems/buddy-strings)

### Solution :

Method 1 (Two Pointer) :
```python
class Solution:
    def buddyStrings(self, s: str, goal: str) -> bool:
        n = len(s)
        if n != len(goal):
            return False

        if s == goal:
            return len(set(s)) < n
        
        pointer_left = 0
        pointer_right = n - 1
        while pointer_left < n and s[pointer_left] == goal[pointer_left]:
            pointer_left += 1
        
        while pointer_right < n and s[pointer_right] == goal[pointer_right]:
            pointer_right -= 1
        
        s = list(s)
        s[pointer_left], s[pointer_right] = s[pointer_right], s[pointer_left]

        return ''.join(s) == goal
```

Method 2 :
```python
class Solution:
    def buddyStrings(self, s: str, goal: str) -> bool:
        n = len(s)
        if n != len(goal):
            return False

        if s == goal:
            return len(set(s)) < n
        
        pointer_left = 0
        pointer_right = n - 1
        while pointer_left < n and s[pointer_left] == goal[pointer_left]:
            pointer_left += 1
        
        while pointer_right < n and s[pointer_right] == goal[pointer_right]:
            pointer_right -= 1
        
        return (s[:pointer_left]+s[pointer_right]+s[pointer_left+1:pointer_right]+s[pointer_left]+s[pointer_right+1:]) == goal
```

![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2734. [Lexicographically Smallest String After Substring Operation](https://leetcode.com/problems/lexicographically-smallest-string-after-substring-operation)

### Solution :

Method 1 (In weekly contest 349) :
```python
class Solution:
    def smallestString(self, s: str) -> str:
        s = list(s)
        start = 0
        a_in_first = s[0] == 'a'
        if a_in_first:
            all_a = True
            for index, ch in enumerate(s):
                if ch != 'a':
                    all_a = False
                    start = index
                    break
            if all_a:
                s[-1] = 'z'
                return ''.join(s)
        
        for index in range(start, len(s)):
            if s[index] == 'a':
                break
            s[index] = chr(ord(s[index]) - 1)
        
        return ''.join(s)
```

Method 2 :
```python
class Solution:
    def smallestString(self, s: str) -> str:
        s = list(s)
        last_cumulative_a_position = 0
        while last_cumulative_a_position < len(s) and s[last_cumulative_a_position] == 'a':
            last_cumulative_a_position += 1
        
        if last_cumulative_a_position == len(s):
            s[-1] = 'z'
            return ''.join(s)

        while last_cumulative_a_position < len(s) and s[last_cumulative_a_position] != 'a':
            s[last_cumulative_a_position] = chr(ord(s[last_cumulative_a_position]) - 1)
            last_cumulative_a_position += 1
        
        return ''.join(s)
```

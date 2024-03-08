![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 455. [Assign Cookies](https://leetcode.com/problems/assign-cookies)

### Solution :

Method 1 :
```python
class Solution:
    def findContentChildren(self, g: List[int], s: List[int]) -> int:
        g.sort()
        s.sort()
        result = 0
        index_g = index_s = 0
        n_g = len(g)
        n_s = len(s)
        while index_g < n_g and index_s < n_s:
            if g[index_g] <= s[index_s]:
                result += 1
                index_g += 1

            index_s += 1

        return result
```

Method 2 :
```python
class Solution:
    def findContentChildren(self, g: List[int], s: List[int]) -> int:
        g.sort()
        s.sort()
        result = 0
        index_s = 0
        n_g = len(g)
        n_s = len(s)
        while result < n_g and index_s < n_s:
            if g[result] <= s[index_s]:
                result += 1

            index_s += 1

        return result
```

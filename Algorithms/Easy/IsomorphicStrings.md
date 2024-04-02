![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 205. [Isomorphic Strings](https://leetcode.com/problems/isomorphic-strings)

### Solution :

Method 1 (Brute Force, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    # Option 1
    def isIsomorphic(self, s: str, t: str) -> bool:
        mapping_s = dict()
        order_s = 0
        temp_s = ''
        for char in s:
            if char not in mapping_s:
                mapping_s[char] = str(order_s)
                order_s += 1

            temp_s += mapping_s[char] + '-'

        mapping_t = dict()
        order_t = 0
        temp_t = ''
        for char in t:
            if char not in mapping_t:
                mapping_t[char] = str(order_t)
                order_t += 1

            temp_t += mapping_t[char] + '-'

        return temp_s == temp_t
    """
    # Option 2

    def isIsomorphic(self, s: str, t: str) -> bool:
        return self.getOrder(s) == self.getOrder(t)

    def getOrder(self, string: str) -> str:
        result = ''

        mapping = dict()
        order = 0
        for char in string:
            if char not in mapping:
                mapping[char] = str(order)
                order += 1

            result += mapping[char] + '-'

        return result
    """
```

![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 165. [Compare Version Numbers](https://leetcode.com/problems/compare-version-numbers)

### Solution :

Method 1 (Hash Map + Bitwise, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def compareVersion(self, version1: str, version2: str) -> int:
        version1 = version1.split(".")
        version2 = version2.split(".")
        n1, n2 = len(version1), len(version2)
        index1 = index2 = 0
        while index1 < n1 or index2 < n2:
            num1 = num2 = 0
            if index1 < n1:
                num1 = int(version1[index1])
            if index2 < n2:
                num2 = int(version2[index2])

            if num1 > num2:
                return 1
            elif num1 < num2:
                return -1

            index1 += 1
            index2 += 1

        return 0
```

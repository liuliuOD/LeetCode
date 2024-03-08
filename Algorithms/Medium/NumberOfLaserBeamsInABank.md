![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2125. [Number Of Laser Beams In A Bank](https://leetcode.com/problems/number-of-laser-beams-in-a-bank)

### Solution :

Method 1 (Time Complexity: $O(M*N)$ (M: length of `bank`, N: length of `bank[0]`), Space Complexity: $O(M)$) :
```python
class Solution:
    def numberOfBeams(self, bank: List[str]) -> int:
        mapping = []
        for row in bank:
            amount = row.count('1')
            if amount:
                mapping.append(amount)

        result = 0
        for index in range(1, len(mapping)):
            result += mapping[index] * mapping[index-1]

        return result
```

Method 2 (Time Complexity: $O(M*N)$ (M: length of `bank`, N: length of `bank[0]`), Space Complexity: $O(1)$) :
```python
class Solution:
    def numberOfBeams(self, bank: List[str]) -> int:
        result = 0
        previous = 0
        for row in bank:
            amount = row.count('1')
            if amount:
                if previous:
                    result += previous * amount
                previous = amount

        return result
```

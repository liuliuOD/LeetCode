![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 997. [Find The Town Judge](https://leetcode.com/problems/find-the-town-judge)

### Solution :

Method 1 (Hash Set + Hash Map, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def findJudge(self, n: int, trust: List[List[int]]) -> int:
        candidates = set(range(1, n+1))
        amount_be_trusted = defaultdict(int)
        for truster, trustee in trust:
            if truster in candidates:
                candidates.remove(truster)
            amount_be_trusted[trustee] += 1

        if not candidates:
            return -1

        result = candidates.pop()
        if amount_be_trusted[result] == n-1:
            return result

        return -1
```

Method 2 (Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```python
```

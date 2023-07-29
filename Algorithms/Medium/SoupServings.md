![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 808. [Soup Servings](https://leetcode.com/problems/soup-servings)

### Solution :

Method 1 (DFS + Memoization) :
```python
class Solution:
    def soupServings(self, n: int) -> float:
        if n >= 4800:
            return 1

        memoization = defaultdict(float)

        return self.dfs(memoization, n, n)

    def dfs(self, memoization: Dict[Tuple[int, int], float], soup_a: int, soup_b: int) -> float:
        if (soup_a, soup_b) in memoization:
            return memoization[(soup_a, soup_b)]

        if soup_a <= 0 and soup_b <= 0:
            return 0.5
        elif soup_a <= 0 and soup_b > 0:
            return 1.0
        elif soup_a > 0 and soup_b <= 0:
            return 0.0
        
        memoization[(soup_a, soup_b)] = 0.25 * sum([self.dfs(memoization, a, b) for a, b in [(soup_a - 100, soup_b), (soup_a - 75, soup_b - 25), (soup_a - 50, soup_b - 50), (soup_a - 25, soup_b - 75)]])
        return memoization[(soup_a, soup_b)]
```

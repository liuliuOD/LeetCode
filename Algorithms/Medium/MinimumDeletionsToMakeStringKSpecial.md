![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 3085. [Minimum Deletions To Make String K-Special](https://leetcode.com/problems/minimum-deletions-to-make-string-k-special)

### Solution :

Method 1 (In weekly contest 389, Brute Force, Time Complexity: $O(N*Log(N))$, Space Complexity: $O(1)$) :
```python
class Solution:
    def minimumDeletions(self, word: str, k: int) -> int:
        BASE = ord('a')
        counter = [0] * 26
        for char in word:
            counter[ord(char)-BASE] += 1

        counter.sort(reverse=True)

        result = inf
        for bound_upper in reversed(range(1, counter[0]+1)):
            temp = 0
            for index in range(26):
                if counter[index] == 0:
                    break

                bound_lower = bound_upper - k
                if counter[index] < bound_lower:
                    temp += counter[index]
                elif counter[index] > bound_upper:
                    temp += counter[index] - bound_upper

            result = min(result, temp)

        return result
```

![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 76. [Minimum Window Substring](https://leetcode.com/problems/minimum-window-substring)

### Solution :

Method 1 (Two Pointer, Time Complexity: $O(M+N)$ (M: length of `s`, N: length of `t`), Space Complexity: $O(M+N)$) :
```python
class Solution:
    def minWindow(self, s: str, t: str) -> str:
        m = len(s)
        n = len(t)
        result = ""
        if m < n:
            return result

        target = Counter(t)
        current = defaultdict(int)
        index_left = index_right = 0
        while index_right < m:
            current[s[index_right]] += 1
            for key, amount in target.items():
                if current[key] < amount:
                    break
            else:
                while index_left <= index_right:
                    temp = s[index_left:index_right+1]
                    if result is '' or len(temp) < len(result):
                        result = temp

                    key_left = s[index_left]
                    if target[key_left] > 0 and current[key_left] <= target[key_left]:
                        break

                    current[key_left] -= 1
                    index_left += 1

            index_right += 1

        return result
```

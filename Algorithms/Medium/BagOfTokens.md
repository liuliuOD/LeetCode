![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 948. [Bag Of Tokens](https://leetcode.com/problems/bag-of-tokens)

### Solution :

Method 1 (Two Pointer, Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$) :
```python
class Solution:
    def bagOfTokensScore(self, tokens: List[int], power: int) -> int:
        tokens.sort()
        left = 0
        right = len(tokens) - 1
        score = 0
        result = 0
        while left <= right:
            if power >= tokens[left]:
                power -= tokens[left]
                left += 1
                score += 1
            elif score > 0:
                power += tokens[right]
                right -= 1
                score -= 1
            else:
                break

            result = max(result, score)

        return result
```

![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 3213. [Construct String With Minimum Cost](https://leetcode.com/problems/construct-string-with-minimum-cost)

### Solution :

Method 1 (Hash Map + Dynamic Programming, Time Complexity: $O(M*N)$, Space Complexity: $O(M+N)$ (M: length of `target`, N: number of the elements in the `words`)) :
```python
BASE = ord('a')

class Solution:
    def minimumCost(self, target: str, words: List[str], costs: List[int]) -> int:
        mapping = [defaultdict(lambda: inf) for _ in range(26)]
        for word, cost in zip(words, costs):
            if word not in target:
                continue

            mapping[ord(word[0])-BASE][word] = min(mapping[ord(word[0])-BASE][word], cost)

        dp = [inf] * len(target)
        for index in range(len(target)):
            if index > 0 and dp[index-1] is inf:
                continue

            candidates = mapping[ord(target[index])-BASE]
            if len(candidates) == 0:
                continue

            for candidate, cost in candidates.items():
                if candidate != target[index:index+len(candidate)]:
                    continue

                dp[index+len(candidate)-1] = min(dp[index+len(candidate)-1], cost + (0 if index == 0 else dp[index-1]))

        return -1 if dp[-1] is inf else dp[-1]
```

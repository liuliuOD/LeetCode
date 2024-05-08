![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 506. [Relative Ranks](https://leetcode.com/problems/relative-ranks)

### Solution :

Method 1 (Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$):
```python
class Solution:
    def findRelativeRanks(self, score: List[int]) -> List[str]:
        n = len(score)
        result: list[str] = [None] * n
        rank = sorted(enumerate(score), key=lambda info: info[1], reverse=True)
        for place, (index, _) in enumerate(rank):
            title: str = str(place+1)
            if place <= 2:
                match place:
                    case 0:
                        title = "Gold Medal"
                    case 1:
                        title = "Silver Medal"
                    case 2:
                        title = "Bronze Medal"

            result[index] = title

        return result
```

Method 2 (Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$):
```python
BASE_MAP = {
    0: "Gold Medal",
    1: "Silver Medal",
    2: "Bronze Medal"
}
class Solution:
    def findRelativeRanks(self, score: List[int]) -> List[str]:
        n = len(score)
        result: list[str] = [None] * n
        rank = sorted(enumerate(score), key=lambda info: info[1], reverse=True)
        for place, (index, _) in enumerate(rank):
            result[index] = BASE_MAP[place] if place <= 2 else str(place+1)

        return result
```

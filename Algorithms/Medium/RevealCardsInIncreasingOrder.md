![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 950. [Reveal Cards In Increasing Order](https://leetcode.com/problems/reveal-cards-in-increasing-order)

### Solution :

Method 1 (Brute Force, Time Complexity: $O(N^2)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def deckRevealedIncreasing(self, deck: List[int]) -> List[int]:
        result = []
        deck.sort(reverse=True)
        for num in deck:
            if len(result) >= 2:
                result = result[-1:] + result[:-1]

            result = [num] + result

        return result
```

Method 2 (Double-ended Queue, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def deckRevealedIncreasing(self, deck: List[int]) -> List[int]:
        result = deque()
        deck.sort(reverse=True)
        for num in deck:
            if len(result) >= 2:
                result.appendleft(result.pop())

            result.appendleft(num)

        return result
```

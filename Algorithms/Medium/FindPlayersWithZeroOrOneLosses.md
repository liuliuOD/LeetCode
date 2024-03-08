![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2225. [Find Players With Zero Or One Losses](https://leetcode.com/problems/find-players-with-zero-or-one-losses)

### Solution :

Method 1 (HashMap + Set, Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$) :
```python
class Solution:
    def findWinners(self, matches: List[List[int]]) -> List[List[int]]:
        mapping_winner = defaultdict(list)
        mapping_loser = defaultdict(list)
        for winner, loser in matches:
            mapping_winner[winner].append(loser)
            mapping_loser[loser].append(winner)

        result = [set(), set()]
        for winner in mapping_winner.keys():
            if len(mapping_loser[winner]) == 0:
                result[0].add(winner)
            elif len(mapping_loser[winner]) == 1:
                result[1].add(winner)

        for loser in mapping_loser.keys():
            if len(mapping_loser[loser]) == 1:
                result[1].add(loser)

        return [sorted(list(item)) for item in result]
```

Method 2 :
```python
class Solution:
    def findWinners(self, matches: List[List[int]]) -> List[List[int]]:
        losers = [0] * 100_001
        for winner, loser in matches:
            if losers[winner] == 0:
                losers[winner] = -1

            if losers[loser] <= 0:
                losers[loser] = 1
            else:
                losers[loser] += 1

        result = [[], []]
        for index, amount_lose in enumerate(losers):
            if amount_lose == -1:
                result[0].append(index)
            elif amount_lose == 1:
                result[1].append(index)

        return result
```

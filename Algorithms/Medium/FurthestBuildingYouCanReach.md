![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1642. [Furthest Building You Can Reach](https://leetcode.com/problems/furthest-building-you-can-reach)

### Solution :

Method 1 (DFS, ERROR: "Memory Limit Exceeded", 11/78) :
```python
class Solution:
    def furthestBuilding(self, buildings: List[int], bricks: int, ladders: int) -> int:
        memoization = defaultdict(int)
        return self.dfs(1, bricks, ladders, memoization, buildings) - 1

    def dfs(self, index: int, bricks: int, ladders: int, memoization, buildings: List[int]) -> int:
        n = len(buildings)
        if index >= n:
            return index

        key = (index, bricks, ladders)
        if key in memoization:
            return memoization[key]

        result = index
        if buildings[index] <= buildings[index-1]:
            result = self.dfs(index+1, bricks, ladders, memoization, buildings)
        else:
            difference = buildings[index] - buildings[index-1]
            if bricks >= difference:
                result = max(result, self.dfs(index+1, bricks-difference, ladders, memoization, buildings))
            if ladders:
                result = max(result, self.dfs(index+1, bricks, ladders-1, memoization, buildings))

        memoization[key] = result
        return result
```

Method 2 (Brute Force, ERROR: "Time Limit Exceeded", 12/78) :
```python
class Solution:
    def furthestBuilding(self, buildings: List[int], bricks: int, ladders: int) -> int:
        n = len(buildings)
        differences = [buildings[index] - buildings[index-1] if buildings[index] > buildings[index-1] else 0 for index in range(1, n)]
        cost_bricks = sum(differences)
        for index in reversed(range(1, n)):
            if cost_bricks <= bricks:
                return index

            base = sorted(differences)
            ladders_current = ladders
            cost_current = cost_bricks
            while ladders_current:
                ladders_current -= 1
                cost_current -= base.pop()
                if cost_current <= bricks:
                    return index

            cost_bricks -= differences.pop()

        return 0
```

Method 3 (Brute Force + Sorting, ERROR: "Time Limit Exceeded", 71/78) :
```python
class Solution:
    def furthestBuilding(self, buildings: List[int], bricks: int, ladders: int) -> int:
        n = len(buildings)
        differences = sorted([buildings[index] - buildings[index-1] if buildings[index] > buildings[index-1] else 0 for index in range(1, n)])
        for index in reversed(range(1, n)):
            if sum(differences[:-ladders] if ladders else differences) <= bricks:
                return index

            target = buildings[index] - buildings[index-1] if buildings[index] > buildings[index-1] else 0
            index_remove = bisect.bisect_left(differences, target)
            differences.pop(index_remove)

        return 0
```

Method 4 :
```python
class Solution:
    def furthestBuilding(self, buildings: List[int], bricks: int, ladders: int) -> int:
        n = len(buildings)
        differences = sorted([buildings[index] - buildings[index-1] if buildings[index] > buildings[index-1] else 0 for index in range(1, n)])
        cost = sum(differences)
        for index in reversed(range(1, n)):
            if ladders and (cost - sum(differences[max(0, len(differences)-ladders):])) <= bricks:
                return index
            elif ladders == 0 and cost <= bricks:
                return index

            target = buildings[index] - buildings[index-1] if buildings[index] > buildings[index-1] else 0
            cost -= target
            index_remove = bisect.bisect_left(differences, target)
            differences.pop(index_remove)

        return 0
```

![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 40. [Combination Sum II](https://leetcode.com/problems/combination-sum-ii)

### Solution :

Method 1 (ERROR: "Memory Limit Exceeded", 172/176) :
```python
class Solution:
    def combinationSum2(self, candidates: List[int], target: int) -> List[List[int]]:
        candidates.sort()
        n = len(candidates)
        self.result = []
        for index_start in range(n):
            selected = [candidates[index_start]]
            self.backtracking(index_start, selected, sum(selected), target, candidates)

        return set(self.result)

    def backtracking(self, index: int, selected: list[int], sum: int, target: int, candidates: list[int]):
        if sum == target:
            self.result.append(tuple(selected))
            return None

        if sum > target:
            return None

        for index_next in range(index+1, len(candidates)):
            value = candidates[index_next]
            selected.append(value)
            sum += value
            self.backtracking(index_next, selected, sum, target, candidates)
            selected.pop()
            sum -= value
```

Method 2 (ERROR: "Time Limit Exceeded", 172/176) :
```python
class Solution:
    def combinationSum2(self, candidates: List[int], target: int) -> List[List[int]]:
        candidates.sort()
        n = len(candidates)
        self.result: set[tuple] = set()
        for index_start in range(n):
            selected = [candidates[index_start]]
            self.backtracking(index_start, selected, sum(selected), target, candidates)

        return self.result

    def backtracking(self, index: int, selected: list[int], sum: int, target: int, candidates: list[int]):
        if sum == target:
            self.result.add(tuple(selected))
            return None

        if sum > target:
            return None

        for index_next in range(index+1, len(candidates)):
            value = candidates[index_next]
            selected.append(value)
            sum += value
            self.backtracking(index_next, selected, sum, target, candidates)
            selected.pop()
            sum -= value
```

Method 3 (Backtracking, Time Complexity: $O(2^N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def combinationSum2(self, candidates: List[int], target: int) -> List[List[int]]:
        candidates.sort()
        n = len(candidates)
        self.result: set[tuple] = set()
        self.backtracking(-1, [], 0, target, candidates)

        return self.result

    def backtracking(self, index: int, selected: list[int], sum: int, target: int, candidates: list[int]):
        if sum == target:
            self.result.add(tuple(selected))
            return None

        if sum > target:
            return None

        for index_next in range(index+1, len(candidates)):
            if index_next > index+1 and candidates[index_next] == candidates[index_next-1]:
                continue

            value = candidates[index_next]
            selected.append(value)
            sum += value
            self.backtracking(index_next, selected, sum, target, candidates)
            selected.pop()
            sum -= value
```

Method 4 (Backtracking, Time Complexity: $O(2^N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def combinationSum2(self, candidates: List[int], target: int) -> List[List[int]]:
        candidates.sort()
        n = len(candidates)
        self.result: set[tuple] = set()
        self.backtracking(-1, [], target, candidates)

        return self.result

    def backtracking(self, index: int, selected: list[int], target: int, candidates: list[int]):
        if target == 0:
            self.result.add(tuple(selected))
            return None

        if target < 0:
            return None

        for index_next in range(index+1, len(candidates)):
            if index_next > index+1 and candidates[index_next] == candidates[index_next-1]:
                continue

            value = candidates[index_next]
            selected.append(value)
            self.backtracking(index_next, selected, target-value, candidates)
            selected.pop()
```

![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2597. [The Number Of Beautiful Subsets](https://leetcode.com/problems/the-number-of-beautiful-subsets)

### Solution :

Method 1 (Bitmask + Brute Force, ERROR: "Time Limit Exceeded", 56 / 1307, Time Complexity: $O(N^2*2^N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def beautifulSubsets(self, nums: List[int], k: int) -> int:
        n = len(nums)
        result = 0
        for bitwise in range(1, 1 << n):
            subset = []
            for index in range(n):
                if ((1 << index) & bitwise) == 0:
                    continue

                for num in subset:
                    if abs(num - nums[index]) == k:
                        break
                else:
                    subset.append(nums[index])
                    continue

                break
            else:
                result += 1
        return result
```

Method 2 (Bitmask + Hash Set, Time Complexity: $O(2^N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def beautifulSubsets(self, nums: List[int], k: int) -> int:
        n = len(nums)
        result = 0
        for bitwise in range(1, 1 << n):
            may_non_beautiful: set[int] = set()
            for index in range(n):
                if ((1 << index) & bitwise) == 0:
                    continue

                current = nums[index]
                if current in may_non_beautiful:
                    break

                may_non_beautiful.add(current - k)
                may_non_beautiful.add(current + k)
            else:
                result += 1
        return result
```

Method 3 (backtracking, Time Complexity: $O(2^N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def beautifulSubsets(self, nums: List[int], k: int) -> int:
        self.result = 0
        memoization = defaultdict(int)
        self.backtracking(0, memoization, nums, k)
        return self.result - 1

    def backtracking(self, index: int, memoization: dict[int, int], nums: list[int], k: int):
        n = len(nums)
        if index >= n:
            self.result += 1
            return

        num = nums[index]
        if num not in memoization:
            add_k = num + k
            minus_k = num - k
            memoization[minus_k] += 1
            memoization[add_k] += 1
            self.backtracking(index+1, memoization, nums, k)
            memoization[minus_k] -= 1
            memoization[add_k] -= 1
            if memoization[minus_k] == 0:
                del memoization[minus_k]
            if memoization[add_k] == 0:
                del memoization[add_k]

        self.backtracking(index+1, memoization, nums, k)
```

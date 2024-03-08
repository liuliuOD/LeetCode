![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2811. [Check If It Is Possible To Split Array](https://leetcode.com/problems/check-if-it-is-possible-to-split-array)

### Solution :

Method 1 (In weekly contest 357, BFS + Memoization) :
```python
class Solution:
    def canSplitArray(self, nums: List[int], m: int) -> bool:
        if len(nums) == 1:
            return True

        visited = set()
        n = len(nums)
        steps = deque([(0, sum(nums), 0, n-1)]) # (current_len, remain, index_left, index_right)
        while steps:
            len_current, sum_remain, index_left, index_right = steps.popleft()
            if (index_left, index_right) in visited:
                continue
            visited.add((index_left, index_right))

            if len_current == n or n-len_current == 2:
                return True
            
            if index_left > index_right:
                continue
            
            if sum_remain-nums[index_left] >= m:
                steps.append((len_current+1, sum_remain-nums[index_left], index_left+1, index_right))

            if sum_remain-nums[index_right] >= m:
                steps.append((len_current+1, sum_remain-nums[index_right], index_left, index_right-1))

        return False
```

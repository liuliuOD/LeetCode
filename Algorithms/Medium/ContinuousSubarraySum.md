![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 523. [Continuous Subarray Sum](https://leetcode.com/problems/continuous-subarray-sum)

### Solution :

Method 1 (Hash Set, ERROR: "Time Limit Exceeded", 94/99, Time Complexity: $O(N^2)$, Space Complexity: $O(N^2)$) :
```python
class Solution:
    def checkSubarraySum(self, nums: List[int], k: int) -> bool:
        n = len(nums)
        sum_subarray = set([nums[0]])
        for index_end in range(1, n):
            temp = set([nums[index_end]])
            for summarize in sum_subarray:
                sum_current = summarize + nums[index_end]
                if sum_current % k == 0:
                    return True

                temp.add(sum_current)

            sum_subarray = temp

        return False
```

Method 2 (Prefix Sum + Hash Map, Time Complexity: $O(N)$, Space Complexity: $O(min(N, K))$) :
```python
class Solution:
    def checkSubarraySum(self, nums: List[int], k: int) -> bool:
        mapping = {}
        prefix_sum = 0
        for index_end in range(len(nums)):
            prefix_sum = (prefix_sum + nums[index_end]) % k
            if index_end > 0 and prefix_sum == 0:
                return True

            if prefix_sum in mapping:
                if index_end - mapping[prefix_sum] >= 2:
                    return True
            else:
                mapping[prefix_sum] = index_end

        return False
```

Method 3 (Prefix Sum + Hash Map, Time Complexity: $O(N)$, Space Complexity: $O(min(N, K))$) :
```python
class Solution:
    def checkSubarraySum(self, nums: List[int], k: int) -> bool:
        mapping = {0: -1}
        prefix_sum = 0
        for index_end in range(len(nums)):
            prefix_sum = (prefix_sum + nums[index_end]) % k
            if prefix_sum in mapping:
                if index_end - mapping[prefix_sum] >= 2:
                    return True
            else:
                mapping[prefix_sum] = index_end

        return False
```

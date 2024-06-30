![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 3202. [Find The Maximum Length Of Valid Subsequence II](https://leetcode.com/problems/find-the-maximum-length-of-valid-subsequence-ii)

### Solution :

Method 1 (ERROR: "Time Limit Exceeded", 709/732) :
```python
import copy

class Solution:
    def maximumLength(self, nums: List[int], k: int) -> int:
        n = len(nums)
        dp = [defaultdict(lambda: 1) for _ in range(k)]
        for index, num in enumerate(nums):
            temp = copy.deepcopy(dp)
            for index_previous in range(index):
                num_previous = nums[index_previous]
                remainder = (num + num_previous) % k
                temp[remainder][num] = max(temp[remainder][num], dp[remainder][num_previous] + 1)

            dp = temp

        return max(max(group.values()) if group.values() else 0 for group in dp)
```

Method 2 (Hash Map, Time Complexity: $O(N^2)$, Space Complexity: $O(N*K)$ (N: number of the elements in `nums`, K: value of `k`)) :
```python
class Solution:
    def maximumLength(self, nums: List[int], k: int) -> int:
        n = len(nums)
        dp = [defaultdict(lambda: 1) for _ in range(n)]
        for index, num in enumerate(nums):
            for index_previous in range(index):
                previous = nums[index_previous]
                remainder = (num + previous) % k
                dp[index][remainder] = max(dp[index][remainder], dp[index_previous][remainder] + 1)

        return max(max(group.values()) for group in dp)
```

Method 3 (Hash Map, Time Complexity: $O(N*K)$, Space Complexity: $O(K^2)$) :
```python
class Solution:
    def maximumLength(self, nums: List[int], k: int) -> int:
        dp = [[0]*k for _ in range(k)]
        result = 1
        for num in nums:
            remainder = num % k
            for offset in range(k):
                remainder_previous = (offset - remainder) % k
                # Option 1
                if 1 + dp[remainder_previous][offset] > dp[remainder][offset]:
                    dp[remainder][offset] = 1 + dp[remainder_previous][offset]
                """
                # Option 2

                dp[remainder][offset] = max(dp[remainder][offset], 1 + dp[remainder_previous][offset])
                """

                # Option 1
                if dp[remainder][offset] > result:
                    result = dp[remainder][offset]
                """
                # Option 2

                result = max(result, dp[remainder][offset])
                """

        return result
```

Method 4 (Array, Time Complexity: $O(N*K)$, Space Complexity: $O(K^2)$) :
```python
class Solution:
    def maximumLength(self, nums: List[int], k: int) -> int:
        dp = [[0]*k for _ in range(k)]
        result = 1
        for num in nums:
            remainder = num % k
            for offset in range(k):
                dp[remainder][offset] = max(dp[remainder][offset], 1 + dp[offset][remainder])

                result = max(result, dp[remainder][offset])

        return result
```

Method 5 ([Array + Reverse Loops](https://leetcode.com/problems/find-the-maximum-length-of-valid-subsequence-ii/solutions/5389350/java-c-python-1d-dp), Time Complexity: $O(N*K)$, Space Complexity: $O(K)$) :
```python
class Solution:
    def maximumLength(self, nums: List[int], k: int) -> int:
        result = 1
        for offset in range(k):
            dp = [0] * k
            for num in nums:
                remainder = num % k
                dp[remainder] = max(dp[remainder], 1 + dp[(offset-remainder)%k])

                if dp[remainder] > result:
                    result = dp[remainder]

        return result
```

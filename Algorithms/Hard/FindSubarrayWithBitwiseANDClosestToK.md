![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 3171. [Find Subarray With Bitwise AND Closest To K](https://leetcode.com/problems/find-subarray-with-bitwise-and-closest-to-k)

### Solution :

Method 1 (Hash Set, Time Complexity: $O(N^2)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def minimumDifference(self, nums: List[int], k: int) -> int:
        n = len(nums)
        dp = [set() for _ in range(n)]
        result = inf
        for index in range(n):
            and_current = nums[index]
            for index_next in range(index, n):
                and_current &= nums[index_next]
                result = min(result, abs(k - and_current))
                if and_current < k or and_current in dp[index_next]:
                    break

                dp[index_next].add(and_current)

        return result
```

Method 2 ([Pruning](https://leetcode.com/problems/find-subarray-with-bitwise-and-closest-to-k/solutions/5243278/pruning-fastest-100-ms), Time Complexity: $O(N*Log(K))$, Space Complexity: $O(N)$) :
```python
class Solution:
    def minimumDifference(self, nums: List[int], k: int) -> int:
        n = len(nums)
        dp = [-inf] * n
        result = inf
        for index in range(n):
            and_current = nums[index]
            for index_next in range(index, n):
                and_current &= nums[index_next]
                result = min(result, abs(k - and_current))
                if and_current < k or and_current <= dp[index_next]:
                    break

                dp[index_next] = and_current

        return result
```

Method 3 (Hash Set, Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def minimumDifference(self, nums: List[int], k: int) -> int:
        and_previous = set()
        result = inf
        for num in nums:
            temp = set([num])
            # Option 1
            for and_num in and_previous:
                temp.add(num & and_num)

            for and_num in temp:
                result = min(result, abs(k - and_num))
            """
            # Option 2

            for and_num in and_previous:
                and_current = num & and_num
                result = min(result, abs(k - and_current))

                if and_num < k:
                    continue

                temp.add(and_current)
            """

            and_previous = temp

        return result
```

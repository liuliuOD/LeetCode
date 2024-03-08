![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2968. [Apply Operations To Maximize Frequency Score](https://leetcode.com/problems/apply-operations-to-maximize-frequency-score)

### Solution :

Method 1 (ERROR: "Time Limit Exceeded", 717/774) :
```python
class Solution:
    def maxFrequencyScore(self, nums: List[int], k: int) -> int:
        n = len(nums)
        nums.sort()
        window = n
        while window > 0:
            for left in range(0, n-window+1):
                median = nums[left+window//2] if window % 2 else round((nums[left+window//2]+nums[left-1+window//2])/2)
                cost = sum([abs(value-median) for value in nums[left:left+window]])
                if cost <= k:
                    return window

            window -= 1

        return 1
```

Method 2 (Binary Search + Prefix Sum) :
```python
class Solution:
    def maxFrequencyScore(self, nums: List[int], k: int) -> int:
        prefix_sum = [0]
        for num in sorted(nums):
            prefix_sum.append(num + prefix_sum[-1])

        n = len(nums)
        left = 1
        right = n
        while left <= right:
            window = left + (right - left)//2
            is_invalid = True
            # Option 1
            for index in range(n-window+1):
                """
                (median * amount_left - sum_left) + (sum_right - median * amount_right)
                => when `amount_left` == `amount_right`, then
                => (median * amount - sum_left) + (sum_right - median * amount)
                => sum_right - sum_left
                """
                if (prefix_sum[index+window] - prefix_sum[index+(window+1)//2]) - (prefix_sum[index+window//2] - prefix_sum[index]) <= k:
                    left = window + 1
                    is_invalid = False
                    break

            if is_invalid:
                right = window - 1
            """
            # Option 2

            for index in range(n-window+1):
                if (prefix_sum[index+window] - prefix_sum[index+(window+1)//2]) - (prefix_sum[index+window//2] - prefix_sum[index]) <= k:
                    left = window + 1
                    break
            else:
                right = window - 1
            """

        return right
```

Method 3 ([Two Pointer](https://leetcode.com/problems/apply-operations-to-maximize-frequency-score/solutions/4419252/explained-with-dry-run-very-simple-easy-to-understand)) :
```python
class Solution:
    def maxFrequencyScore(self, nums: List[int], k: int) -> int:
        nums.sort()
        operations = 0
        result = 0
        left = right = 0
        while right < len(nums):
            operations += nums[right] - nums[(left+right)//2]
            while operations > k:
                operations += nums[left] - nums[(left+right+1)//2]
                left += 1

            result = max(result, right - left + 1)
            right += 1

        return result
```

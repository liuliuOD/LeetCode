![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 930. [Binary Subarrays With Sum](https://leetcode.com/problems/binary-subarrays-with-sum)

### Solution :

Method 1 (Prefix Sum, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def numSubarraysWithSum(self, nums: List[int], goal: int) -> int:
        frequency = defaultdict(int)
        summarize = 0
        result = 0
        for num in nums:
            summarize += num
            if summarize-goal in frequency:
                result += frequency[summarize-goal]
            if summarize == goal:
                result += 1

            frequency[summarize] += 1

        return result
```

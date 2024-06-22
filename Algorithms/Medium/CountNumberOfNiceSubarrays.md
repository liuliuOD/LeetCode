![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1248. [Count Number Of Nice Subarrays](https://leetcode.com/problems/count-number-of-nice-subarrays)

### Solution :

Method 1 (Mathematic, Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def numberOfSubarrays(self, nums: List[int], k: int) -> int:
        n = len(nums)
        index_odds = list(filter(lambda index: nums[index] % 2 == 1, range(n)))
        result = 0
        for index, index_odd in enumerate(index_odds):
            if index < k-1:
                continue

            left = 1
            if index == k-1:
                left += index_odds[0]
            else:
                left += index_odds[index-k+1] - index_odds[index-k] - 1

            right = 1
            if index == len(index_odds)-1:
                right += n - index_odds[-1] - 1
            else:
                right += index_odds[index+1] - index_odds[index] - 1

            result += left * right

        return result
```

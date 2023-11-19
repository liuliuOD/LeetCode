![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1887. [Reduction Operations To Make The Array Elements Equal](https://leetcode.com/problems/reduction-operations-to-make-the-array-elements-equal)

### Solution :

Method 1 (Time Complexity: $O(N*Log(N))$, Space Complexity: $O()$ (doesn't use any extra space, so the `SC` depends on the implementation of each programming language)) :
```python
class Solution:
    def reductionOperations(self, nums: List[int]) -> int:
        nums.sort()

        n = len(nums)
        result = 0
        for index in range(n-1):
            if nums[index] != nums[index+1]:
                result += n - 1 - index

        return result
```

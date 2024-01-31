![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 3020. [Find The Maximum Number Of Elements In Subset](https://leetcode.com/problems/find-the-maximum-number-of-elements-in-subset)

### Solution :

Method 1 (Hash Map, Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$) :
```python
class Solution:
    def maximumLength(self, nums: List[int]) -> int:
        mapping = defaultdict(int)
        # Option 1
        for num in sorted(nums):
            mapping[num] += 1

        result = 0
        for key in mapping.keys():
        """
        # Option 2

        for num in nums:
            mapping[num] += 1

        result = 0
        for key in sorted(mapping.keys()):
        """
            if key == 1:
                result = mapping[key] if mapping[key] % 2 == 1 else mapping[key] - 1
                continue

            temp = 0
            key_target = key
            while key_target in mapping and mapping[key_target] > 0:
                if mapping[key_target] == 1:
                    temp += 1
                    mapping[key_target] = 0
                    break

                temp += 2
                mapping[key_target] = 0
                key_target *= key_target

            if temp % 2 == 0:
                temp -= 1
            result = max(result, temp)

        return result
```

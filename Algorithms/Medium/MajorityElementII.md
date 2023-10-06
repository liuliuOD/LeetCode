![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 229. [Majority Element II](https://leetcode.com/problems/majority-element-ii)

### Solution :

Method 1 (Hash Map) :
```python
class Solution:
    def majorityElement(self, nums: List[int]) -> List[int]:
        n = len(nums)
        threshold = n // 3
        mapping = defaultdict(int)
        result = set()
        for num in nums:
            mapping[num] += 1
            if num not in result and mapping[num] > threshold:
                result.add(num)

        return list(result)
```

Method 2 (Boyer-Moore Majority Voting Algorithm, Space Complexity: $O(1)$) :
```python
class Solution:
    def majorityElement(self, nums: List[int]) -> List[int]:
        """
        The frequency needs to be greater than ⌊n / 3⌋ in order for at most two numbers in 'nums' to meet the requirements.
        """
        result_1 = result_2 = None
        frequency_1 = frequency_2 = 0
        for num in nums:
            # We need to check if 'num' equal to 'result_1' or 'result_2' first in order to avoid a situation where 'result_1' equals 'result_2'.
            if num == result_1:
                frequency_1 += 1
            elif num == result_2:
                frequency_2 += 1

            elif result_1 is None or frequency_1 == 0:
                result_1 = num
                frequency_1 = 1
            elif result_2 is None or frequency_2 == 0:
                result_2 = num
                frequency_2 = 1

            else:
                frequency_1 -= 1
                frequency_2 -= 1

        frequency_1 = frequency_2 = 0
        for num in nums:
            if num == result_1:
                frequency_1 += 1
            elif num == result_2:
                frequency_2 += 1

        n = len(nums)
        threshold = n // 3
        result = []
        if frequency_1 > threshold:
            result.append(result_1)
        if frequency_2 > threshold:
            result.append(result_2)

        return result
```

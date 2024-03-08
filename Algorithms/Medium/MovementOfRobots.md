![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2731. [Movement Of Robots](https://leetcode.com/problems/movement-of-robots)

### Solution :

Method 1 (Change Moving Direction, ERROR: "Time Limit Exceeded") :
```python
class Solution:
    def sumDistance(self, nums: List[int], s: str, d: int) -> int:
        MOD = 10**9+7
        for _ in range(d):
            mapping = defaultdict(list)
            for index in range(len(nums)):
                target = nums[index] + 1 if s[index] == 'R' else nums[index] - 1
                mapping[target].append(index)
                nums[index] = target
            for k, item in mapping.items():
                if len(item) > 1:
                    for i in item:
                        s = list(s)
                        s[i] = 'R' if s[i] == 'L' else 'L'
                        s = ''.join(s)
        result = 0
        for i in range(len(nums)):
            for j in range(i+1, len(nums)):
                result = (result + (abs(nums[i] - nums[j]) % MOD)) % MOD
        return result
```

Method 2 (Force Sum, ERROR: "Time Limit Exceeded") :
```python
class Solution:
    def sumDistance(self, nums: List[int], s: str, d: int) -> int:
        MOD = 10**9+7
        for index in range(len(nums)):
            nums[index] += d if s[index] == 'R' else -d
        result = 0
        for i in range(len(nums)):
            for j in range(i+1, len(nums)):
                result = (result + (abs(nums[i] - nums[j]) % MOD)) % MOD
        return result
```

Method 3 (Order Positions from smallest to largest) :
```python
class Solution:
    def sumDistance(self, nums: List[int], s: str, d: int) -> int:
        for index in range(len(nums)):
            nums[index] += d if s[index] == 'R' else -d

        MOD = 10**9+7
        nums.sort()
        result = 0
        substract = nums[0]
        """
        When nums is unordered list, we need to use abs() to get positive distances.
        If ordered nums to increasing order, we can calculate distance by simply substract each items.
        eg:
          unordered nums = [3, -1, 2], then distances need to use abs() like this:
          result = abs(-1 - 3) + abs(2 - 3) + abs(2 - (-1)) 

          ordered nums = [-1, 2, 3], then distances like this:
          result = (2 - (-1)) + (3 - (-1)) + (3 - 2) = (2 * 1 - (-1)) + (3 * 2 - (-1 + 2))
        """
        for index in range(1, len(nums)):
            result = (result + nums[index] * index % MOD - substract) % MOD
            substract = (substract + nums[index]) % MOD
        return result
```

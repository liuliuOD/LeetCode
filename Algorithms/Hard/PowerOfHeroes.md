![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2681. [Power Of Heroes](https://leetcode.com/problems/power-of-heroes)

### Solution :

Method 1 (Cache, ERROR: "Time Limit Exceeded" in 2573 / 2582) :
```python
class Solution:
    def sumOfPower(self, nums: List[int]) -> int:
        nums.sort()

        MOD = 10**9 + 7
        result = 0
        quadratics = {}
        for i in range(len(nums)):
            if i in quadratics:
                qua = quadratics[i]
            else:
                qua = quadratics[i] = nums[i]**2 % MOD
            result = (result + nums[i] * qua) % MOD

        power = {}
        for left in range(len(nums)):
            for right in range(left+1, len(nums)):
                qua = quadratics[right]
                bit_num = right - left - 1
                if bit_num in power:
                    bit = power[bit_num]
                else:
                    bit = power[bit_num] = 2**bit_num % MOD
                result = (result + nums[left] * qua * bit) % MOD
        return result
```

[Method 2 (Math)](https://leetcode.com/problems/power-of-heroes/solutions/3520233/c-java-python-sort-and-enumerate-each-maximum-value/) :
```python
class Solution:
    def sumOfPower(self, nums: List[int]) -> int:
        MOD = 10**9 + 7
        temp = 0
        result = 0
        for num in sorted(nums):
            result = (result + (temp + num) * num**2) % MOD
            temp = (temp * 2 + num) % MOD
        return result
```

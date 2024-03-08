![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 137. [Single Number II](https://leetcode.com/problems/single-number-ii)

### Solution :

Method 1 (Brute Force) :
```python
class Solution:
    def singleNumber(self, nums: List[int]) -> int:
        result = set()
        counter = defaultdict(int)
        for num in nums:
            counter[num] += 1
            if counter[num] > 1 and num in result:
                result.remove(num)
            elif counter[num] == 1:
                result.add(num)
        
        return list(result)[0]
```

Method 2 ([Bitwise](https://leetcode.com/problems/single-number-ii/solutions/3714928/bit-manipulation-c-java-python-beginner-friendly/)) :
```python
class Solution:
    def singleNumber(self, nums: List[int]) -> int:
        once = 0
        twice = 0
        for num in nums:
            once = (once^num) & (~twice)
            twice = (twice^num) & (~once)
        
        return once
```

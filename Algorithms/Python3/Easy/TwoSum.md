## [Two Sum](https://leetcode.com/problems/two-sum)

### Solution :

Method 1 :
```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        map = {}
        for index, num in enumerate(nums):
            if (indice := map.get(target - num)) is not None:
                return [index, indice]
            map[num] = index
```

Method 2 :
```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        map = {}
        for index, num in enumerate(nums):
            if (target - num) in map:
                return [index, map[target - num]]
            map[num] = index
```

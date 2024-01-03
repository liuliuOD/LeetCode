![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2610. [Convert An Array Into A 2D Array With Conditions](https://leetcode.com/problems/convert-an-array-into-a-2d-array-with-conditions)

### Solution :

Method 1 (Hash Map, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def findMatrix(self, nums: List[int]) -> List[List[int]]:
        mapping = defaultdict(int)
        for num in nums:
            mapping[num] += 1

        result = []
        while mapping.values():
            key_drop = []
            temp = []
            for key in mapping.keys():
                temp.append(key)

                mapping[key] -= 1
                if mapping[key] == 0:
                    key_drop.append(key)

            result.append(temp)

            for key in key_drop:
                del mapping[key]

        return result
```

Method 2 (Time Complexity: $O(N^2)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def findMatrix(self, nums: List[int]) -> List[List[int]]:
        result = []
        for num in nums:
            for index_x in range(len(result)):
                if num in result[index_x]:
                    continue

                result[index_x].append(num)
                break
            else:
                result.append([num])

        return result
```

Method 3 (Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def findMatrix(self, nums: List[int]) -> List[List[int]]:
        # Option 1
        frequency = defaultdict(int)
        """
        # Option 2

        n = len(nums)
        frequency = [0] * (n + 1)
        """
        result = []
        for num in nums:
            if frequency[num] >= len(result):
                result.append([])
            result[frequency[num]].append(num)

            frequency[num] += 1

        return result
```

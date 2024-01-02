![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2610. [Convert An Array Into A 2D Array With Conditions](https://leetcode.com/problems/convert-an-array-into-a-2d-array-with-conditions)

### Solution :

Method 1 (Hash Map) :
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

Method 2 :
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

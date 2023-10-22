![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2910. [Minimum Number Of Groups To Create A Valid Assignment](https://leetcode.com/problems/minimum-number-of-groups-to-create-a-valid-assignment)

### Solution :

Method 1 (DFS + Memoization) :
```python
class Solution:
    def minGroupsForValidAssignment(self, nums: List[int]) -> int:
        n = len(nums)
        counter = Counter(nums)
        if len(counter) == 1:
            return 1

        minimum = min(counter.values())
        memoization = {}
        result = inf
        for m in range(1, minimum+1):
            temp = 0
            for target in counter.values():
                temp_amount = self.sumAmount(target, m, m+1, memoization)
                if temp_amount != inf:
                    temp += temp_amount
                    continue

                temp = inf
                break
            result = min(result, temp)

        return result

    def sumAmount(self, target, m, n, memoization) -> int:
        key = f'{target}-{m}-{n}'
        if key in memoization:
            return memoization[key]

        if target == 0:
            return 0
        elif target < 0:
            return inf

        # find the minimum by minus `m` or `n`
        result = min(1+self.sumAmount(target-n, n, m, memoization), 1+self.sumAmount(target-m, n, m, memoization))
        memoization[key] = result

        return memoization[key]
```

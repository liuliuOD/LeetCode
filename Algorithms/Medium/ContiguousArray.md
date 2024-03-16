![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
![language-Go](https://img.shields.io/badge/Go-00add8?style=for-the-badge&logo=GO&logoColor=white)
---

## 525. [Contiguous Array](https://leetcode.com/problems/contiguous-array)

### Solution :

Method 1 (Prefix Sum, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def findMaxLength(self, nums: List[int]) -> int:
        prefix_sum = [0]
        for num in nums:
            if num == 0:
                prefix_sum.append(prefix_sum[-1]-1)
            else:
                prefix_sum.append(prefix_sum[-1]+1)

        mapping = defaultdict(list)
        for index, amount in enumerate(prefix_sum):
            mapping[amount].append(index)

        return max([group[-1]-group[0] if len(group) > 1 else 0 for group in mapping.values()])
```

Method 2 (Prefix Sum, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def findMaxLength(self, nums: List[int]) -> int:
        prefix_sum = [0]
        mapping = defaultdict(list)
        mapping[0].append(0)
        for num in nums:
            if num == 0:
                prefix_sum.append(prefix_sum[-1]-1)
            else:
                prefix_sum.append(prefix_sum[-1]+1)

            mapping[prefix_sum[-1]].append(len(prefix_sum)-1)

        return max([group[-1]-group[0] if len(group) > 1 else 0 for group in mapping.values()])
```

Method 3 (Prefix Sum, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def findMaxLength(self, nums: List[int]) -> int:
        prefix_sum = [0]
        mapping = defaultdict(list)
        mapping[0].append(0)
        result = 0
        for num in nums:
            if num == 0:
                prefix_sum.append(prefix_sum[-1]-1)
            else:
                prefix_sum.append(prefix_sum[-1]+1)

            current = mapping[prefix_sum[-1]]
            current.append(len(prefix_sum)-1)

            if len(current) > 1:
                result = max(result, current[-1]-current[0])

        return result
```

Method 4 (Prefix Sum, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def findMaxLength(self, nums: List[int]) -> int:
        cumulative = 0
        mapping = {0: -1}
        result = 0
        for index, num in enumerate(nums):
            if num == 0:
                cumulative -= 1
            else:
                cumulative += 1

            if cumulative in mapping:
                result = max(result, index - mapping[cumulative])
            else:
                mapping[cumulative] = index

        return result
```

### Solution :

Method 1 (Prefix Sum, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```go
func findMaxLength(nums []int) int {
    result := 0
    mapping := make(map[int]int)
    mapping[0] = -1
    cumulative := 0
    for index, num := range nums {
        if num == 0 {
            cumulative++
        } else {
            cumulative--
        }

        /* Option 1 */
        value, ok := mapping[cumulative]
        if ok {
        /* Option 2

        if value, ok := mapping[cumulative]; ok {
        */
            result = max(result, index - value)
        } else {
            mapping[cumulative] = index
        }
    }

    return result
}
```
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
![language-Go](https://img.shields.io/badge/Go-00add8?style=for-the-badge&logo=GO&logoColor=white)
---

## 442. [Find All Duplicates In An Array](https://leetcode.com/problems/find-all-duplicates-in-an-array)

### Constraints:

- Write an algorithm that runs in $O(N)$ time.
- Uses only constant extra space.

### Solution :

Method 1 (Hash Set, Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def findDuplicates(self, nums: List[int]) -> List[int]:
        result = set()
        for index in range(len(nums)):
            nums[abs(nums[index])-1] *= -1
            if nums[abs(nums[index])-1] > 0:
                result.add(abs(nums[index]))

        return list(result)
```

### Solution :

Method 1 (Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```go
func findDuplicates(nums []int) []int {
    var result []int
    for _, num := range nums {
        num_abs := num
        if num_abs < 0 {
            num_abs *= -1
        }
        nums[num_abs-1] *= -1

        if nums[num_abs-1] > 0 {
            result = append(result, num_abs)
        }
    }

    return result
}
```

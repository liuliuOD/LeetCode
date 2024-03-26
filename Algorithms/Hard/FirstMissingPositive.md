![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
![language-Go](https://img.shields.io/badge/Go-00add8?style=for-the-badge&logo=GO&logoColor=white)
---

## 41. [First Missing Positive](https://leetcode.com/problems/first-missing-positive)

### Constraints:

- Runs in $O(N)$ time.
- Uses $O(1)$ auxiliary space.

### Solution :

Method 1 (Hash Set, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def firstMissingPositive(self, nums: List[int]) -> int:
        nums_set = set(nums)
        for candidate in range(1, len(nums_set)+2):
            if candidate in nums_set:
                continue

            return candidate
```

### Solution :

Method 1 (Array, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```go
func firstMissingPositive(nums []int) int {
    n := len(nums)
    visited := make([]bool, n)
    for index := 0; index < n; index++ {
        visited = append(visited, false)
    }

    for _, num := range nums {
        if num <= 0 || num > n {
            continue
        }

        visited[num-1] = true
    }

    for index, seen := range visited {
        if seen == false {
            return index + 1
        }
    }

    return n + 1
}
```

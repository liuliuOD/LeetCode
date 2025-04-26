![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2444. [Count Subarrays With Fixed Bounds](https://leetcode.com/problems/count-subarrays-with-fixed-bounds)

### Solution :

Method 1 (Time Complexity: $O(N)$, Space Complexity: $O(1)$ (N: the number of the elements in `nums`)) :
```rust
impl Solution {
    pub fn count_subarrays(nums: Vec<i32>, min_k: i32, max_k: i32) -> i64 {
        let mut index_min: i32 = -1;
        let mut index_max: i32 = -1;
        let mut index_start: i32 = 0;
        let mut result: i64 = 0;

        for (index, &num) in nums.iter().enumerate() {
            let index = index as i32;

            // If num is out of bounds, reset the window
            if num < min_k || num > max_k {
                index_start = index + 1;
                index_min = -1;
                index_max = -1;
            }

            // Update indices where min_k and max_k are found
            if num == min_k {
                index_min = index;
            }
            if num == max_k {
                index_max = index;
            }

            // If both min_k and max_k are found, count subarrays
            if index_min > -1 && index_max > -1 {
                result += (index_min.min(index_max) - index_start + 1) as i64;
            }
        }

        return result
    }
}
```

### Solution :

Method 1 (Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def countSubarrays(self, nums: List[int], minK: int, maxK: int) -> int:
        index_min = index_max = -1
        index_start = 0
        result = 0
        for index, num in enumerate(nums):
            if num < minK or num > maxK:
                index_start = index + 1
                index_min = index_max = -1

            if num == minK:
                index_min = index
            if num == maxK:
                index_max = index

            if index_min > -1 and index_max > -1:
                result += min(index_min, index_max) - index_start + 1

        return result
```

### Solution :

Method 1 (Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```go
func countSubarrays(nums []int, minK int, maxK int) int64 {
    indexMin, indexMax, indexStart := -1, -1, 0
    result := 0
    for index, num := range nums {
        if num < minK || num > maxK {
            indexStart = index + 1
            indexMin = -1
            indexMax = -1
        }

        if num == minK {
            indexMin = index
        }
        if num == maxK {
            indexMax = index
        }

        if indexMin > -1 && indexMax > -1 {
            result += min(indexMin, indexMax) - indexStart + 1
        }
    }

    return int64(result)
}
```

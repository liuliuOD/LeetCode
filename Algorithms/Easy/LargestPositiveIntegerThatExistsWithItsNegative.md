![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
![language-Go](https://img.shields.io/badge/Go-00add8?style=for-the-badge&logo=GO&logoColor=white)
---

## 2441. [Largest Positive Integer That Exists With Its Negative](https://leetcode.com/problems/largest-positive-integer-that-exists-with-its-negative)

### Solution :

Method 1 (Hash Set, Time Complexity: $O(N*Log(N))$, Space Complexity: $O(1)$) :
```rust
use std::cmp::Ordering;
impl Solution {
    pub fn find_max_k(mut nums: Vec<i32>) -> i32 {
        let mut left: usize = 0;
        let mut right: usize = nums.len() - 1;
        nums.sort();
        while left < right {
            match (nums[left] + nums[right]).cmp(&0) {
                Ordering::Equal => return nums[right],
                Ordering::Less => left += 1,
                Ordering::Greater => right -= 1,
            };
        }

        return -1
    }
}
```

### Solution :

Method 1 (Hash Set, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def findMaxK(self, nums: List[int]) -> int:
        mapping = set()
        result = -1
        for num in nums:
            mapping.add(num)
            if -num in mapping:
                result = max(result, abs(num))

        return result
```

### Solution :

Method 1 (Hash Map, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```go
func findMaxK(nums []int) int {
    var result int = -1
    var mapping map[int]bool = make(map[int]bool)
    for _, num := range nums {
        mapping[num] = true
        _, ok := mapping[-num]
        if num < 0 {
            num = -num
        }
        if ok && num > result {
            result = num
        }
    }

    return result
}
```

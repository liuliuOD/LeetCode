![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 153. [Find Minimum In Rotated Sorted Array](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array)

### Constraints:

- You must write an algorithm that runs in `O(log n)` time.

### Solution :

Method 1 (Binary Search) :
```rust
impl Solution {
    pub fn find_min(nums: Vec<i32>) -> i32 {
        let n: usize = nums.len();
        let mut left: usize = 0;
        let mut right: usize = n;
        while left < right {
            let middle: usize = left + (right-left)/2;
            /* Option 1 */
            if nums[middle] < nums[0] {
                right = middle;
            } else {
                left = middle + 1;
            }
            /* Option 2

            match nums[middle] < nums[0] {
                true => right = middle,
                _ => left = middle + 1,
            };
            */
        }

        return match left < n {
            true => nums[left],
            _ => nums[0]
        }
    }
}
```

Method 2 (Binary Search) :
```rust
impl Solution {
    pub fn find_min(nums: Vec<i32>) -> i32 {
        let n: usize = nums.len();
        let mut left: usize = 0;
        let mut right: usize = n - 1;
        while left < right {
            let middle: usize = left + (right-left)/2;
            match nums[middle] <= nums[right] {
                true => right = middle,
                _ => left = middle + 1,
            };
        }

        /* Option 1 */
        return nums[right]
        /* Option 2

        return nums[left]
        */
    }
}
```

Method 3 :
```rust
impl Solution {
    pub fn find_min(nums: Vec<i32>) -> i32 {
        return nums.into_iter().min().unwrap()
    }
}
```

### Solution :

Method 1 (Binary Search, Time Complexity: $O(Log(N))$, Space Complexity: $O(1)$) :
```python
class Solution:
    def findMin(self, nums: List[int]) -> int:
        n = len(nums)
        left = 0
        right = n - 1
        while left <= right:
            middle = left + (right-left)//2
            if nums[middle] < nums[0]:
                right = middle - 1
            else:
                left = middle + 1

        return nums[left] if left < n else nums[0]
```

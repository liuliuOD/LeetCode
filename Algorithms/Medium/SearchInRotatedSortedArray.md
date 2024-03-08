![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 33. [Search In Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array)

### Solution :

Method 1 (Binary Search) :
```rust
impl Solution {
    pub fn search(nums: Vec<i32>, target: i32) -> i32 {
        let pivot: usize = Self::find_pivot(&nums);

        return Self::binary_search(pivot, target, &nums)
    }

    fn find_pivot(nums: &Vec<i32>) -> usize {
        let n: usize = nums.len();
        // If we use rightest item as baseline, we should prevent right = n. Because when n = 2, we would find middle = 1 at first time and then jump out while loop.
        let rightest: i32 = nums[n-1];
        let mut left: usize = 0;
        let mut right: usize = n - 1;
        while left <= right && right < n {
            let middle: usize = left + (right - left) / 2;

            if nums[middle] < rightest {
                right = middle - 1;
            }
            else if nums[middle] > rightest {
                left = middle + 1;
            }
            else if nums[middle] == rightest {
                break;
            }
        }

        return left
    }

    fn binary_search(pivot: usize, target: i32, nums: &Vec<i32>) -> i32 {
        let n: usize = nums.len();
        let mut left: usize = 0;
        let mut right: usize = n;
        while left < right {
            let middle: usize = left + (right-left)/2;
            let index: usize = (middle + pivot) % n;
            if nums[index] == target {
                return index as _
            }
            else if nums[index] > target {
                right = middle;
            }
            else if nums[index] < target {
                left = middle + 1;
            }
        }

        return -1
    }
}
```

### Solution :

Method 1 (Binary Search) :
```python
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        pivot = self.findPivotIndex(nums)
        left = 0
        right = len(nums)
        while left <= right:
            middle_ordered = left + (right - left) // 2
            middle_nums = (middle_ordered + pivot) % len(nums)
            if nums[middle_nums] == target:
                return middle_nums
            elif nums[middle_nums] > target:
                right = middle_ordered - 1
            elif nums[middle_nums] < target:
                left = middle_ordered + 1
        return -1

    def findPivotIndex(self, nums: List[int]) -> int:
        tail = nums[-1]
        left = 0
        right = len(nums) - 1
        while left <= right:
            middle = left + (right - left) // 2
            if nums[middle] > tail:
                left = middle + 1
            else:
                right = middle - 1
        return left
```

Method 2 (Binary Search) :
```python
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        pivot = self.findPivot(nums)

        return self.binarySearch(nums, pivot, target)

    def findPivot(self, nums: List[int]) -> int:
        pointer_left = 0
        pointer_right = len(nums)
        # If we use leftest item as baseline, we should prevent pointer_right = n-1. Because when n = 2, we would find middle = 0 at first time and then jump out while loop.
        target = nums[0]
        while pointer_left < pointer_right:
            middle = pointer_left + (pointer_right-pointer_left)//2

            if nums[middle] == target:
                return middle
            elif nums[middle] > target:
                pointer_left = middle + 1
            elif nums[middle] < target:
                pointer_right = middle

            target = nums[middle]
        return pointer_left

    def binarySearch(self, nums: List[int], pivot: int, target: int) -> int:
        n = len(nums)
        pointer_left = 0
        pointer_right = n - 1
        while pointer_left <= pointer_right:
            middle = pointer_left + (pointer_right-pointer_left)//2

            index = (middle+pivot) % n
            if nums[index] == target:
                return index
            elif nums[index] > target:
                pointer_right = middle - 1
            elif nums[index] < target:
                pointer_left = middle + 1

        return -1
```

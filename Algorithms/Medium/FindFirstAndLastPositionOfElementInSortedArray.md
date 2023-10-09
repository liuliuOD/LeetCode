![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
![language-PHP](https://img.shields.io/badge/%20-PHP-acb1f9?style=for-the-badge&logo=PHP)
---

## 34. [Find First And Last Position Of Element In Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array)

### Constraints:

- You must write an algorithm with $O(log(N))$ runtime complexity.

### Solution :

Method 1 (Binary Search) :
```python
class Solution:
    def searchRange(self, nums: List[int], target: int) -> List[int]:
        start = -1
        end = -1
        left = 0
        right = len(nums) - 1
        while left <= right:
            middle = left + (right - left) // 2
            if nums[middle] < target:
                left = middle + 1
            else:
                right = middle - 1
        if left < len(nums) and nums[left] == target:
            start = left

        left = 0
        right = len(nums) - 1
        while left <= right:
            middle = left + (right - left) // 2
            if nums[middle] <= target:
                left = middle + 1
            else:
                right = middle - 1
        if right >= 0 and nums[right] == target:
            end = right

        return [start, end]
```

### Solution :

Method 1 (Binary Search) :
```php
class Solution {

    /**
     * @param Integer[] $nums
     * @param Integer $target
     * @return Integer[]
     */
    function searchRange($nums, $target) {
        $n = count($nums);

        $left = 0;
        $right = $n;
        while ($left < $right) {
            $index = $left + intval(($right - $left) / 2);

            if ($nums[$index] < $target) {
                $left = $index + 1;
            } else if ($nums[$index] >= $target) {
                $right = $index;
            }
        }

        if (
            $left >= $n
            || $nums[$left] !== $target
        ) {
            return [-1, -1];
        }

        $result = [$left];
        $left = 0;
        $right = $n - 1;
        while ($left <= $right) {
            $index = $left + intval(($right - $left) / 2);

            if ($nums[$index] <= $target) {
                $left = $index + 1;
            } else if ($nums[$index] > $target) {
                $right = $index - 1;
            }
        }
        $result[] = $right;

        return $result;
    }
}
```

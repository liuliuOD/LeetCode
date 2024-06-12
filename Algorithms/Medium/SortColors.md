![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 75. [Sort Colors](https://leetcode.com/problems/sort-colors)

```
You must solve this problem without using the library's sort function.
```

### Follow Up:

- Could you come up with a one-pass algorithm using only constant extra space?

### Solution :

Method 1 (Two Pointer, Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```rust
impl Solution {
    pub fn sort_colors(nums: &mut Vec<i32>) {
        let mut left: usize = 0;
        let mut right: usize = nums.len() - 1;
        let mut index: usize = 0;
        while index <= right && right > 0 {
            match nums[index] {
                0 => {
                    nums.swap(index, left);
                    left += 1;
                    index += 1;
                },
                1 => {
                    index += 1;
                },
                2 | _ => {
                    nums.swap(index, right);
                    right -= 1;
                },
            };
        }
    }
}
```

### Solution :

Method 1 (Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def sortColors(self, nums: List[int]) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        n = len(nums)
        index_current = 0
        for color in range(3):
            for index in range(n):
                if nums[index] == color:
                    nums[index_current], nums[index] = nums[index], nums[index_current]
                    index_current += 1

            if index_current >= n:
                break
```

Method 2 (Counting Sort, Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```python
BASE = 3

class Solution:
    def sortColors(self, nums: List[int]) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        colors = [0] * BASE
        for num in nums:
            colors[num] += 1

        prefix_sum = 0
        for index in range(BASE):
            while colors[index]:
                nums[prefix_sum] = index
                prefix_sum += 1
                colors[index] -= 1
```

Method 3 (Two Pointer, Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def sortColors(self, nums: List[int]) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        left, right = 0, len(nums)-1
        index = 0
        while index <= right:
            if nums[index] == 0:
                nums[left], nums[index] = nums[index], nums[left]
                left += 1
                index += 1
            elif nums[index] == 1:
                index += 1
            elif nums[index] == 2:
                nums[right], nums[index] = nums[index], nums[right]
                right -= 1
```

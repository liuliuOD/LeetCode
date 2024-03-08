![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 852. [Peak Index In A Mountain Array](https://leetcode.com/problems/peak-index-in-a-mountain-array)

### Solution :

Method 1 (Binary Search) :
```rust
impl Solution {
    pub fn peak_index_in_mountain_array(arr: Vec<i32>) -> i32 {
        let mut pointer_left: usize = 0;
        let mut pointer_right: usize = arr.len();
        while pointer_left < pointer_right {
            let middle: usize = pointer_left + (pointer_right - pointer_left) / 2;

            if arr[middle] < arr[middle+1] {
                pointer_left = middle + 1;
            } else if arr[middle] > arr[middle+1] {
                pointer_right = middle;
            }
        }

        return pointer_right as _
    }
}
```

### Solution :

Method 1 (Binary Search) :
```python
class Solution:
    def peakIndexInMountainArray(self, arr: List[int]) -> int:
        pointer_left = 0
        pointer_right = len(arr) - 1
        while pointer_left <= pointer_right:
            middle = pointer_left + (pointer_right - pointer_left) // 2

            if arr[middle] < arr[middle+1]:
                pointer_left = middle + 1
            elif arr[middle] > arr[middle+1]:
                pointer_right = middle - 1

        return pointer_left
```

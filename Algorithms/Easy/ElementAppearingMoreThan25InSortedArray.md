![language-RUST](https://img.shields.io/badge/%20-RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1287. [Element Appearing More Than 25% In Sorted Array](https://leetcode.com/problems/element-appearing-more-than-25-in-sorted-array)

### Solution :

Method 1 (Sliding Window) :
```rust
impl Solution {
    pub fn find_special_integer(arr: Vec<i32>) -> i32 {
        let n: usize = arr.len();
        let window: usize = n / 4;
        for index in 0..n {
            if arr[index] == arr[index+window] {
                return arr[index]
            }
        }

        unreachable!()
    }
}
```

Method 2 (Binary Search) :
```rust
impl Solution {
    pub fn find_special_integer(arr: Vec<i32>) -> i32 {
        let n: usize = arr.len();
        for index in 1..=3 {
            let current: i32 = arr[n*index/4];

            let mut left: usize = 0;
            let mut right: usize = n;
            while left < right {
                let middle: usize = left + (right-left)/2;
                if arr[middle] > current {
                    right = middle;
                } else {
                    left = middle + 1;
                }
            }
            let index_right: usize = right;

            let mut left: usize = 0;
            let mut right: usize = n;
            while left < right {
                let middle: usize = left + (right-left)/2;
                if arr[middle] >= current {
                    right = middle;
                } else {
                    left = middle + 1;
                }
            }
            let index_left: usize = left;

            if (index_right-index_left) > n/4 {
                return current
            }
        }

        unreachable!()
    }
}
```

### Solution :

Method 1 (Hash Map, Time Complexity: $O(N*Log(N))$, Space Complexity: $O(1)$) :
```python
class Solution:
    def findSpecialInteger(self, arr: List[int]) -> int:
        n = len(arr)
        mapping = defaultdict(int)
        for item in arr:
            mapping[item] += 1
            if mapping[item] > n / 4:
                return item
```

Method 2 (Binary Search, Time Complexity: $O(N*Log(N))$, Space Complexity: $O(1)$) :
```python
class Solution:
    def findSpecialInteger(self, arr: List[int]) -> int:
        n = len(arr)
        candidates = set(arr)
        for candidate in candidates:
            # Option 1
            index_left, index_right = None, None

            left = 0
            right = n
            while left < right:
                middle = left + (right - left)//2
                if arr[middle] < candidate:
                    left = middle + 1
                else:
                    right = middle
            index_left = left

            left = 0
            right = n
            while left < right:
                middle = left + (right - left)//2
                if arr[middle] <= candidate:
                    left = middle + 1
                else:
                    right = middle
            index_right = right
            """
            # Option 2

            index_left = bisect.bisect_left(arr, candidate)
            index_right = bisect.bisect_right(arr, candidate)
            """

            if (index_right-index_left) > n/4:
                return candidate
```

Method 3 (Binary Search, Time Complexity: $O(Log(N))$, Space Complexity: $O(1)$) :
```python
class Solution:
    def findSpecialInteger(self, arr: List[int]) -> int:
        n = len(arr)
        candidates = [arr[n*position//4] for position in range(1, 4)]
        for candidate in candidates:
            # Option 1
            index_left, index_right = None, None

            left = 0
            right = n
            while left < right:
                middle = left + (right - left)//2
                if arr[middle] < candidate:
                    left = middle + 1
                else:
                    right = middle
            index_left = left

            left = 0
            right = n
            while left < right:
                middle = left + (right - left)//2
                if arr[middle] <= candidate:
                    left = middle + 1
                else:
                    right = middle
            index_right = right
            """
            # Option 2

            index_left = bisect.bisect_left(arr, candidate)
            index_right = bisect.bisect_right(arr, candidate)
            """

            if (index_right-index_left) > n/4:
                return candidate
```

Method 4 (Sliding Window) :
```python
class Solution:
    def findSpecialInteger(self, arr: List[int]) -> int:
        n = len(arr)
        window = n // 4
        for index in range(n-window):
            if arr[index] == arr[index+window]:
                return arr[index]
```

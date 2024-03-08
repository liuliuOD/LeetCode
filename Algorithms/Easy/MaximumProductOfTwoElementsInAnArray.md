![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1464. [Maximum Product Of Two Elements In An Array](https://leetcode.com/problems/maximum-product-of-two-elements-in-an-array)

### Solution :

Method 1 :
```rust
impl Solution {
    pub fn max_product(mut nums: Vec<i32>) -> i32 {
        nums.sort();

        return (nums.pop().unwrap()-1) * (nums.pop().unwrap()-1)
    }
}
```

Method 2 :
```rust
impl Solution {
    pub fn max_product(nums: Vec<i32>) -> i32 {
        let mut maximum_1: i32 = 0;
        let mut maximum_2: i32 = 0;
        for num in nums {
            if num >= maximum_1 {
                std::mem::swap(&mut maximum_1, &mut maximum_2);
                maximum_1 = num;
            } else if num > maximum_2 {
                maximum_2 = num;
            }
        }

        return (maximum_1 - 1) * (maximum_2 - 1)
    }
}
```

### Solution :

Method 1 (Time Complexity: $O(N*Log(N))$, Space Complexity: $O()$ (doesn't use any extra space, so the `SC` depends on the implementation of each programming language, eg: Java -> $O(Log(N))$, C++ -> $O(Log(N))$, Python -> $O(N)$)) :
```python
class Solution:
    def maxProduct(self, nums: List[int]) -> int:
        nums.sort()

        return (nums[-1]-1) * (nums[-2]-1)
```

Method 2 (Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def maxProduct(self, nums: List[int]) -> int:
        maximum = 0
        maximum_second = 0
        for num in nums:
            if num >= maximum:
                maximum, maximum_second = num, maximum
            elif num > maximum_second:
                maximum_second = num

        return (maximum-1) * (maximum_second-1)
```

Method 3 (Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$) :
```python
class Solution:
    def maxProduct(self, nums: List[int]) -> int:
        nums = [-num for num in nums]
        heapq.heapify(nums)

        return (-heapq.heappop(nums)-1) * (-heapq.heappop(nums)-1)
```

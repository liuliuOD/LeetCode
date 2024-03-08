![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1913. [Maximum Product Difference Between Two Pairs](https://leetcode.com/problems/maximum-product-difference-between-two-pairs)

### Solution :

Method 1 :
```rust
impl Solution {
    pub fn max_product_difference(mut nums: Vec<i32>) -> i32 {
        nums.sort();

        let n: usize = nums.len();
        return nums[n-1]*nums[n-2] - nums[0]*nums[1]
    }
}
```

Method 2 :
```rust
impl Solution {
    pub fn max_product_difference(mut nums: Vec<i32>) -> i32 {
        let mut maximum: i32 = 0;
        let mut maximum_2: i32 = 0;
        let mut minimum: i32 = 10_000;
        let mut minimum_2: i32 = 10_000;
        for num in nums {
            if num > maximum {
                std::mem::swap(&mut maximum, &mut maximum_2);
                maximum = num;
            } else if num > maximum_2 {
                maximum_2 = num;
            }

            if num < minimum {
                std::mem::swap(&mut minimum, &mut minimum_2);
                minimum = num;
            } else if num < minimum_2 {
                minimum_2 = num;
            }
        }

        return maximum*maximum_2 - minimum*minimum_2
    }
}
```

### Solution :

Method 1 (Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$) :
```python
class Solution:
    def maxProductDifference(self, nums: List[int]) -> int:
        nums.sort()

        return nums[-1]*nums[-2] - nums[0]*nums[1]
```

Method 2 (Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def maxProductDifference(self, nums: List[int]) -> int:
        maximum = 0
        maximum_2 = 0
        minimum = inf
        minimum_2 = inf
        for num in nums:
            if num > maximum:
                maximum, maximum_2 = num, maximum
            elif num > maximum_2:
                maximum_2 = num

            if num < minimum:
                minimum, minimum_2 = num, minimum
            elif num < minimum_2:
                minimum_2 = num

        return maximum*maximum_2 - minimum*minimum_2
```

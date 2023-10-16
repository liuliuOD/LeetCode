![language-RUST](https://img.shields.io/badge/%20-RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 238. [Product Of Array Except Self](https://leetcode.com/problems/product-of-array-except-self)

### Solution :

Method 1 (Prefix Sum + Suffix Sum) :
```rust
impl Solution {
    pub fn product_except_self(nums: Vec<i32>) -> Vec<i32> {
        let n: usize = nums.len();
        // Option 1
        let mut result: Vec<i32> = vec![1];
        for index in 1..n {
            result.push(result[index-1]*nums[index-1]);
        }
        /* Option 2

        let mut result: Vec<i32> = vec![1; n];
        for index in 1..n {
            result[index] = result[index-1] * nums[index-1];
        }
        */

        let mut product: i32 = 1;
        for index in (0..n).rev() {
            result[index] *= product;
            product *= nums[index];
        }

        return result
    }
}
```

### Solution :

Method 1 (Prefix Sum + Suffix Sum, Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def productExceptSelf(self, nums: List[int]) -> List[int]:
        n = len(nums)
        result = [1] * n

        for index in range(n):
            result[index] = result[index] * (1 if index == 0 else nums[index-1]*result[index-1])

        product = 1
        for index in reversed(range(n)):
            result[index] = result[index] * product
            product *= nums[index]

        return result
```

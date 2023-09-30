![language-RUST](https://img.shields.io/badge/%20-RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## [132 Pattern](https://leetcode.com/problems/132-pattern)

### Solution :

Method 1 ([Monotonic Stack](https://leetcode.com/problems/132-pattern/solutions/3517952/explain-why-we-can-use-monotonic-stack-here)) :
```rust
impl Solution {
    pub fn find132pattern(nums: Vec<i32>) -> bool {
        let mut stack: Vec<i32> = vec![];
        let mut num_right_largest_smaller_current: i32 = i32::MIN;

        for index in (0..nums.len()).rev() {
            if nums[index] < num_right_largest_smaller_current {
                return true
            }
            while !stack.is_empty() && nums[index] > *stack.last().unwrap() {
                num_right_largest_smaller_current = stack.pop().unwrap();
            }
            stack.push(nums[index]);
        }
        false
    }
}
```

### Solution :

Method 1 ([Monotonic Stack](https://ayoubomari.medium.com/132-pattern-1b890c763bd5)) :
```python
class Solution:
    def find132pattern(self, nums: List[int]) -> bool:
        stack = []
        for num in nums:
            if not stack:
                stack.append((num, num))
                continue

            minimum = num
            while stack and stack[-1][1] < num:
                minimum = min(minimum, stack.pop()[0])

            if stack and stack[-1][0] < num < stack[-1][1]:
                return True

            stack.append((minimum, num))

        return False
```

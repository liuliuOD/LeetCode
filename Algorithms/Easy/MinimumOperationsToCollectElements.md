![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2869. [Minimum Operations To Collect Elements](https://leetcode.com/problems/minimum-operations-to-collect-elements)

### Solution :

Method 1 :
```rust
impl Solution {
    pub fn min_operations(nums: Vec<i32>, k: i32) -> i32 {
        let n: usize = nums.len();
        let target: i64 = (1 << k) - 1;
        let mut mask: i64 = 0;
        for index in (0..n).rev() {
            mask |= (1 << (nums[index]-1));
            if (mask & target) == target {
                return (n - index) as _
            }
        }

        /* Option 1 */
        return 0 as _
        /* Option 2

        unreachable!()
        */
    }
}
```

### Solution :

Method 1 (Set, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def minOperations(self, nums: List[int], k: int) -> int:
        target = set(list(range(1, k+1)))
        result = 0
        for num in reversed(nums):
            result += 1

            if num in target:
                target.remove(num)

            if len(target) == 0:
                return result
```

Method 2 (Bitmask, Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def minOperations(self, nums: List[int], k: int) -> int:
        n = len(nums)
        target = (1 << k) - 1
        mask = 0
        for index in reversed(range(n)):
            mask |= 1 << (nums[index]-1)
            if (mask & target) == target:
                return n - index
```

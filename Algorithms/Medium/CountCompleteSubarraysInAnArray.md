![language-RUST](https://img.shields.io/badge/%20-RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2799. [Count Complete Subarrays In An Array](https://leetcode.com/problems/count-complete-subarrays-in-an-array)

### Solution :

Method 1 (HashSet) :
```rust
use std::collections::HashSet;
use std::iter::FromIterator;
impl Solution {
    pub fn count_complete_subarrays(nums: Vec<i32>) -> i32 {
        let n: usize = nums.len();
        let mut distinct: HashSet<i32> = HashSet::from_iter(nums.iter().cloned());
        let mut result: i32 = 0;

        for index in 0..n {
            let mut subarray: HashSet<i32> = HashSet::new();
            for index_next in index..n {
                subarray.insert(nums[index_next]);

                if subarray.len() != distinct.len() {
                    continue;
                }

                result += (n - index_next) as i32;
                break;
            }
        }

        return result
    }
}
```

### Solution :

Method 1 (Set) :
```python
class Solution:
    def countCompleteSubarrays(self, nums: List[int]) -> int:
        n = len(nums)
        distinct = set(nums)
        result = 0

        for left in range(n):
            temp = set([nums[left]])
            for right in range(left, n):
                temp.add(nums[right])
                if len(temp) == len(distinct):
                    result += n - right
                    break

        return result
```

![language-RUST](https://img.shields.io/badge/%20-RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2741. [Special Permutations](https://leetcode.com/problems/special-permutations)

### Solution :

Method 1 (Bitmask) :
```rust
use std::collections::HashMap;

const MOD: i32 = (10 as i32).pow(9) + 7;
impl Solution {
    pub fn special_perm(nums: Vec<i32>) -> i32 {
        let n: usize = nums.len();
        let mut dp: HashMap<(usize, usize), i32> = HashMap::new();
        let mut result: i32 = 0;
        for index in 0..n {
            result = (result + Self::dfs(index, &nums, &mut dp, 1<<index)) % MOD;
        }

        return result
    }

    fn dfs(index_previous: usize, nums: &Vec<i32>, dp: &mut HashMap<(usize, usize), i32>, mask: usize) -> i32 {
        let n = nums.len();
        if mask == ((1<<n) - 1) {
            return 1
        }

        if dp.contains_key(&(index_previous, mask)) {
            return *dp.get(&(index_previous, mask)).unwrap()
        }

        let mut permutation_amount: i32 = 0;
        for index_target in 0..n {
            let mask_target = 1<<index_target;
            if (mask & mask_target) != 0 {
                continue;
            }

            if nums[index_previous] % nums[index_target] == 0 || nums[index_target] % nums[index_previous] == 0 {
                let mask_next = mask | mask_target;
                let temp: i32 = Self::dfs(index_target, nums, dp, mask_next);

                dp.insert((index_target, mask_next), temp);
                permutation_amount = (permutation_amount + temp) % MOD;
            }
        }

        return permutation_amount
    }
}
```

### Solution :

Method 1 (Bitmask) :
```python
MOD = 10**9 + 7
class Solution:
    def specialPerm(self, nums: List[int]) -> int:
        self.nums = nums
        self.n = len(nums)
        result = 0
        for index in range(self.n):
            result = (result + self.bitMask(index, 1<<index)) % MOD
        return result
    
    @cache
    def bitMask(self, index_previous: int, mask: int) -> int:
        if mask == ((1<<self.n) - 1):
            return 1
        
        permutation_amount = 0
        for index_target in range(self.n):
            mask_target = 1<<index_target
            if mask_target & mask is not 0:
                continue
            
            if self.nums[index_previous] % self.nums[index_target] == 0 or self.nums[index_target] % self.nums[index_previous] == 0:
                permutation_amount = (permutation_amount + self.bitMask(index_target, mask | mask_target)) % MOD
        return permutation_amount
```

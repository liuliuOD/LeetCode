![language-RUST](https://img.shields.io/badge/%20-RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1512. [Number Of Good Pairs](https://leetcode.com/problems/number-of-good-pairs)

### Solution :

Method 1 :
```rust
impl Solution {
    pub fn num_identical_pairs(nums: Vec<i32>) -> i32 {
        let n: usize = nums.len();
        let mut result: i32 = 0;
        for i in 0..n {
            for j in i+1..n {
                if nums[i] == nums[j] {
                    result += 1;
                }
            }
        }

        return result
    }
}
```

Method 2 (Hash Map) :
```rust
use std::collections::HashMap;

impl Solution {
    pub fn num_identical_pairs(nums: Vec<i32>) -> i32 {
        let mut mapping: HashMap<i32, i32> = HashMap::new();
        let mut result: i32 = 0;
        for num in nums {
            // Option 1
            if mapping.contains_key(&num) {
                result += mapping[&num];
            }

            // here we add 1 if num exist in mapping, set mapping[num] = 1 when num not exist.
            mapping.entry(num).and_modify(|val| *val += 1).or_insert(1);
            """
            // Option 2

            let val = mapping.entry(num).or_insert(0);
            result += *val;
            *val += 1;
            """
            """
            // Option 3

            let val = mapping.entry(num).or_default();
            result += *val;
            *val += 1;
            """
        }

        return result
    }
}
```

### Solution :

Method 1 (Loop, Time Complexity: $O(N^2)$) :
```python
class Solution:
    def numIdenticalPairs(self, nums: List[int]) -> int:
        n = len(nums)
        result = 0
        for i in range(n):
            for j in range(i+1, n):
                if nums[i] == nums[j]:
                    result += 1

        return result
```

Method 2 (Hash Map, Time Complexity: $O(N)$) :
```python
class Solution:
    def numIdenticalPairs(self, nums: List[int]) -> int:
        result = 0
        mapping = defaultdict(int)
        for num in nums:
            # Option 1
            if num in mapping:
                result += mapping[num]

            mapping[num] += 1
            """
            # Option 2

            result += mapping[num]
            mapping[num] += 1
            """

        return result
```

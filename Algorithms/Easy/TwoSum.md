![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## [Two Sum](https://leetcode.com/problems/two-sum)

### Solution :

Method 1 (bubble sort, slow and less memory) :
```rust
impl Solution {
  pub fn two_sum(nums: Vec<i32>, target: i32) -> Vec<i32> {
    for i in 0..(nums.len() - 1) {
      for j in i+1..nums.len() {
        if nums[i] + nums[j] == target {
          return vec![i as i32, j as i32]
        }
      }
    }

    vec![0, 0]
  }
}
```

Method 2 (Hash Map, fast and more memory) :
```rust
use std::collections::HashMap;

impl Solution {
  pub fn two_sum(nums: Vec<i32>, target: i32) -> Vec<i32> {
    let mut hm = HashMap::with_capacity(nums.len());

    for (index, &item) in nums.iter().enumerate() {
      match hm.get(&item) {
        Some(&another_index) => return vec![index as i32, another_index as i32],
        None => {
          hm.insert(target - &item, index);
        },
      }
    }
    vec![0, 0]
  }
}
```

### Solution :

Method 1 :
```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        map = {}
        for index, num in enumerate(nums):
            if (indice := map.get(target - num)) is not None:
                return [index, indice]
            map[num] = index
```

Method 2 :
```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        map = {}
        for index, num in enumerate(nums):
            if (target - num) in map:
                return [index, map[target - num]]
            map[num] = index
```

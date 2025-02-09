![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2364. [Count Number Of Bad Pairs](https://leetcode.com/problems/count-number-of-bad-pairs)

### Hint :

```text
j - i != nums[j] - nums[i]
can be transferred to
j - nums[j] != i - nums[i]
```

### Solution :

Method 1 (Time Complexity: $O(N^2)$, Space Complexity: $O(1)$ (N: the number of elements in `nums`)) :
```rust
impl Solution {
    pub fn count_bad_pairs(nums: Vec<i32>) -> i64 {
        let n: usize = nums.len();
        let mut result: i64 = 0;
        for index_right in 1..n {
            for index_left in 0..index_right {
                if nums[index_right]-nums[index_left] == (index_right-index_left) as i32 {
                    continue;
                }

                result += 1;
            }
        }

        return result
    }
}
```

Method 2 (Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```rust
use std::collections::HashMap;

impl Solution {
    pub fn count_bad_pairs(nums: Vec<i32>) -> i64 {
        let mut result: i64 = 0;
        let mut mapping: HashMap<i64, i64> = HashMap::new();
        for (index, &num) in nums.iter().enumerate() {
            let index: i64 = index as i64;
            let key: i64 = index - num as i64;
            let item: &mut i64 = mapping.entry(key).or_default();
            *item += 1;
            result += index + 1 - *item;
        }

        return result
    }
}
```

Method 3 (total amount of pairs minus amount of good pairs, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```rust
use std::collections::HashMap;

impl Solution {
    pub fn count_bad_pairs(nums: Vec<i32>) -> i64 {
        let mut amount_good_pair: i64 = 0;
        let mut mapping: HashMap<i64, i64> = HashMap::new();
        for (index, &num) in nums.iter().enumerate() {
            let index: i64 = index as i64;
            let key: i64 = index - num as i64;
            let item: &mut i64 = mapping.entry(key).or_default();
            amount_good_pair += *item;
            *item += 1;
        }

        let n: i64 = nums.len() as i64;
        return n*(n-1)/2 - amount_good_pair
    }
}
```

Method 4 (total amount of pairs minus amount of good pairs, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```rust
use std::collections::HashMap;

impl Solution {
    pub fn count_bad_pairs(nums: Vec<i32>) -> i64 {
        let n: usize = nums.len();
        let mut counter: HashMap<i32, i64> = HashMap::new();
        let mut result: i64 = 0;
        for index in 0..n {
            let good: i32 = index as i32 - nums[index];
            result += index as i64 - match counter.get(&good) {
                Some(value) => *value,
                _ => 0,
            };

            *counter.entry(good).or_insert(0) += 1;
        }

        return result
    }
}
```

### Solution :

Method 1 :
```python
class Solution:
    def countBadPairs(self, nums: List[int]) -> int:
        n = len(nums)
        mapping = defaultdict(int)
        result = 0
        for index in range(n):
            key = index - nums[index]
            mapping[key] += 1
            result += index + 1 - mapping[key]

        return result
```

Method 2 :
```python
class Solution:
    def countBadPairs(self, nums: List[int]) -> int:
        n = len(nums)
        mapping = defaultdict(int)
        amount_of_good_pairs = 0
        for index in range(n):
            key = index - nums[index]
            amount_of_good_pairs += mapping[key]
            mapping[key] += 1

        return n*(n-1)//2 - amount_of_good_pairs
```

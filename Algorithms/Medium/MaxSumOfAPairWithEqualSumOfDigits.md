![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 2342. [Max Sum Of A Pair With Equal Sum Of Digits](https://leetcode.com/problems/max-sum-of-a-pair-with-equal-sum-of-digits)

### Solution :

Method 1 (Hash Map, Time Complexity: $O(N)$, Space Complexity: $O(N*Log(N))$ (N: the number of elements in `nums`)) :
```rust
use std::collections::HashMap;

impl Solution {
    pub fn maximum_sum(nums: Vec<i32>) -> i32 {
        let mut mapping: HashMap<i32, Vec<i32>> = HashMap::new();
        for num in nums {
            let mut sum_of_digits: i32 = 0;
            let mut temp: i32 = num;
            while temp > 0 {
                sum_of_digits += temp % 10;
                temp /= 10;
            }
            mapping.entry(sum_of_digits).or_default().push(num);
        }

        let mut result: i32 = -1;
        for group in mapping.values_mut() {
            if group.len() < 2 {
                continue;
            }

            group.sort();
            result = i32::max(result, group[group.len()-1]+group[group.len()-2]);
        }

        return result
    }
}
```

Method 2 (Hash Map, Time Complexity: $O(N)$, Space Complexity: $O(Log(M))$ (M: the maximum number in `nums`, N: the number of elements in `nums`)) :
```rust
use std::collections::HashMap;

impl Solution {
    pub fn maximum_sum(nums: Vec<i32>) -> i32 {
        let mut mapping: HashMap<i32, Vec<i32>> = HashMap::new();
        for num in nums {
            let mut sum_of_digits: i32 = 0;
            let mut temp: i32 = num;
            while temp > 0 {
                sum_of_digits += temp % 10;
                temp /= 10;
            }
            mapping.entry(sum_of_digits).and_modify(|pair| {
                if num > pair[0] && num > pair[1] {
                    if pair[0] > pair[1] {
                        pair[1] = num;
                    } else {
                        pair[0] = num;
                    }
                } else if num > pair[0] {
                    pair[0] = num;
                } else if num > pair[1] {
                    pair[1] = num;
                }
            }).or_insert(Vec::from([num, i32::MIN]));
        }

        let mut result: i32 = -1;
        for pair in mapping.values() {
            result = i32::max(result, pair.into_iter().sum());
        }

        return result
    }
}
```

Method 3 (Hash Map, Time Complexity: $O(N)$, Space Complexity: $O(Log(M))$ (M: the maximum number in `nums`, N: the number of elements in `nums`)) :
```rust
use std::collections::HashMap;

impl Solution {
    pub fn maximum_sum(nums: Vec<i32>) -> i32 {
        let mut result: i32 = -1;
        let mut mapping: HashMap<i32, i32> = HashMap::new();
        for num in nums {
            let mut sum_of_digits: i32 = 0;
            let mut temp: i32 = num;
            while temp > 0 {
                sum_of_digits += temp % 10;
                temp /= 10;
            }
            mapping.entry(sum_of_digits).and_modify(|current| {
                result = i32::max(result, *current + num);
                if num > *current {
                    *current = num;
                }
            }).or_insert(num);
        }

        return result
    }
}
```

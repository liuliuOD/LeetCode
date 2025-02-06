![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 1726. [Tuple With Same Product](https://leetcode.com/problems/tuple-with-same-product)

### Solution :

Method 1 (Brute Force, Time Complexity: $O(N^2)$, Space Complexity: $O(N^2)$ (N: the number of elements in `nums`)) :
```rust
use std::collections::HashMap;

impl Solution {
    pub fn tuple_same_product(nums: Vec<i32>) -> i32 {
        let n: usize = nums.len();
        let mut mapping: HashMap<i32, Vec<(usize, usize)>> = HashMap::new();
        for left in 0..n {
            for right in left+1..n {
                let pair: (usize, usize) = (left, right);
                mapping.entry(nums[left]*nums[right]).and_modify(|group| group.push(pair)).or_insert(Vec::from([pair]));
            }
        }

        let mut result: i32 = 0;
        for key in mapping.keys() {
            let group: &Vec<(usize, usize)> = mapping.get(key).unwrap();
            let amount: usize = group.len();
            if amount <= 1 {
                continue;
            }

            for index in 0..amount {
                for index_next in index+1..amount {
                    if group[index].0 == group[index_next].0 || group[index].0 == group[index_next].1 || group[index].1 == group[index_next].0 || group[index].1 == group[index_next].1 {
                        continue;
                    }

                    result += 8;
                }
            }
        }

        return result
    }
}
```

Method 2 (Brute Force, Time Complexity: $O(N^2)$, Space Complexity: $O(N^2)$ (N: the number of elements in `nums`)) :
```rust
use std::collections::HashMap;

impl Solution {
    pub fn tuple_same_product(nums: Vec<i32>) -> i32 {
        let n: usize = nums.len();
        let mut mapping: HashMap<i32, Vec<(usize, usize)>> = HashMap::new();
        for left in 0..n {
            for right in left+1..n {
                let pair: (usize, usize) = (left, right);
                mapping.entry(nums[left]*nums[right]).and_modify(|group| group.push(pair)).or_insert(Vec::from([pair]));
            }
        }

        let mut result: i32 = 0;
        for key in mapping.keys() {
            let group: &Vec<(usize, usize)> = mapping.get(key).unwrap();
            let amount: usize = group.len();
            if amount <= 1 {
                continue;
            }

            result += (amount*(amount-1)*4) as i32;
        }

        return result
    }
}
```

Method 2 (Brute Force + Optimization, Time Complexity: $O(N^2)$, Space Complexity: $O(N)$ (N: the number of elements in `nums`)) :
```rust
use std::collections::HashMap;

impl Solution {
    pub fn tuple_same_product(nums: Vec<i32>) -> i32 {
        let n: usize = nums.len();
        let mut mapping: HashMap<i32, i32> = HashMap::new();
        for left in 0..n {
            for right in left+1..n {
                mapping.entry(nums[left]*nums[right]).and_modify(|amount| *amount += 1).or_insert(1);
            }
        }

        let mut result: i32 = 0;
        for key in mapping.keys() {
            let amount: i32 = *mapping.get(key).unwrap();
            if amount <= 1 {
                continue;
            }

            result += amount * (amount-1) * 4;
        }

        return result
    }
}
```

Method 3 (Brute Force + Optimization, Time Complexity: $O(N^2)$, Space Complexity: $O(N)$ (N: the number of elements in `nums`)) :
```rust
use std::collections::HashMap;

impl Solution {
    pub fn tuple_same_product(nums: Vec<i32>) -> i32 {
        let n: usize = nums.len();
        let mut mapping: HashMap<i32, i32> = HashMap::new();
        let mut result: i32 = 0;
        for left in 0..n {
            for right in left+1..n {
                let product: i32 = nums[left] * nums[right];
                if let Some(amount) = mapping.get(&product) {
                    result += *amount;
                }

                mapping.entry(product).and_modify(|amount| *amount += 1).or_insert(1);
            }
        }

        return result * 8
    }
}
```

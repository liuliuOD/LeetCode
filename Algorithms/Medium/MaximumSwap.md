![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 670. [Maximum Swap](https://leetcode.com/problems/maximum-swap)

### Solution :

Method 1 (Hash Map, Time Complexity: $O(N^2)$, Space Complexity: $O(N)$ (N: the amount of digits in `num`)) :
```rust
use std::collections::HashMap;

impl Solution {
    pub fn maximum_swap(mut num: i32) -> i32 {
        let mut num_list: Vec<i32> = Vec::new();
        let mut mapping: HashMap<i32, Vec<usize>> = HashMap::new();
        let mut index: usize = 0;
        while num > 0 {
            let digit: i32 = num % 10;
            num_list.push(digit);
            mapping.entry(digit).and_modify(|group| group.push(index)).or_insert(Vec::from([index]));
            index += 1;
            num /= 10;
        }

        let n: usize = num_list.len();
        for index in (1..n).rev() {
            for digit in (num_list[index]+1..=9).rev() {
                if !mapping.contains_key(&digit) {
                    continue;
                }

                for &index_digit in mapping[&digit].iter() {
                    if index_digit >= index {
                        continue;
                    }

                    num_list.swap(index, index_digit);
                    return Self::get_result(num_list)
                }
            }
        }

        return Self::get_result(num_list)
    }

    fn get_result(mut num_list: Vec<i32>) -> i32 {
        num_list.reverse();
        return num_list.iter().fold(0, |accumulative, digit| accumulative*10 + digit)
    }
}
```

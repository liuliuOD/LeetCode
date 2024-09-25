![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 3043. [Find The Length Of The Longest Common Prefix](https://leetcode.com/problems/find-the-length-of-the-longest-common-prefix)

### Solution :

Method 1 (Hash Set, Time Complexity: $O((M+N)*K)$, Space Complexity: $O(M*K)$ (M: the number of the elements in `arr1`, N: the number of the elements in `arr2`, K: the average digits of each element in `arr1` and `arr2`)) :
```rust
use std::collections::HashSet;

impl Solution {
    pub fn longest_common_prefix(arr1: Vec<i32>, arr2: Vec<i32>) -> i32 {
        let mut set: HashSet<i32> = HashSet::new();
        for element in arr1 {
            let mut prefix: i32 = 0;
            for digit in Self::get_digits(element).into_iter() {
                prefix = prefix*10 + digit;
                set.insert(prefix);
            }
        }

        let mut result: i32 = 0;
        for element in arr2 {
            let mut prefix: i32 = 0;
            for (index, digit) in Self::get_digits(element).into_iter().enumerate() {
                prefix = prefix*10 + digit;
                if !set.contains(&prefix) {
                    break;
                }

                result = i32::max(result, (index+1) as i32);
            }
        }

        return result
    }

    fn get_digits(num: i32) -> Vec<i32> {
        return num.to_string()
            .chars()
            .map(|d| d.to_digit(10).unwrap() as i32)
            .collect::<Vec<_>>()
    }
}
```

Method 2 (Hash Set, Time Complexity: $O((M+N)*K)$, Space Complexity: $O(M*K)$ (M: the number of the elements in `arr1`, N: the number of the elements in `arr2`, K: the average digits of each element in `arr1` and `arr2`)) :
```rust
use std::collections::HashSet;

impl Solution {
    pub fn longest_common_prefix(arr1: Vec<i32>, arr2: Vec<i32>) -> i32 {
        let mut set: HashSet<i32> = HashSet::new();
        for mut element in arr1 {
            while element > 0 {
                set.insert(element);
                element /= 10;
            }
        }

        let mut result: i32 = 0;
        for mut element in arr2 {
            while element > 0 {
                if set.contains(&element) {
                    result = i32::max(result, element.to_string().len() as i32);
                }

                element /= 10;
            }
        }

        return result
    }
}
```

![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 2191. [Sort The Jumbled Numbers](https://leetcode.com/problems/sort-the-jumbled-numbers)

### Solution :

Method 1 (Time Complexity: $O(N*Log(N)*M)$, Space Complexity: $O(N)$ (M: the average digits count of the elements in `nums`, N: the number of the elements in `nums`)) :
```rust
impl Solution {
    pub fn sort_jumbled(mapping: Vec<i32>, mut nums: Vec<i32>) -> Vec<i32> {
        nums.sort_by_key(|&num| {
            if num == 0 {
                return mapping[num as usize]
            }

            let mut num_temp: i32 = num;
            let mut num_mapped: i32 = 0;
            let mut digit: u32 = 0;
            while num_temp > 0 {
                let num_current: i32 = num_temp % 10;
                num_mapped += mapping[num_current as usize] * 10_i32.pow(digit);
                digit += 1;
                num_temp /= 10;
            }
            return num_mapped
        });

        return nums
    }
}
```

Method 2 (Time Complexity: $O(N*(Log(N)+M))$, Space Complexity: $O(N)$ (M: the average digits count of the elements in `nums`, N: the number of the elements in `nums`)) :
```rust
impl Solution {
    pub fn sort_jumbled(mapping: Vec<i32>, mut nums: Vec<i32>) -> Vec<i32> {
        nums.sort_by_cached_key(|&num| {
            let mut num = num;
            if num == 0 {
                return mapping[num as usize]
            }

            let mut num_mapped: i32 = 0;
            let mut position: u32 = 0;
            while num > 0 {
                let num_current: i32 = num % 10;
                num_mapped += mapping[num_current as usize] * 10_i32.pow(position);
                position += 1;
                num /= 10;
            }
            return num_mapped
        });

        return nums
    }
}
```

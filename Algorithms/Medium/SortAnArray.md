![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 912. [Sort An Array](https://leetcode.com/problems/sort-an-array)

### Solution :

Method 1 (Counting Sort, Time Complexity: $(10^5)$, Space Complexity: $O(10^5)$) :
```rust
const AMOUNT: usize = 50_000;
const AMOUNT_LENGTH: usize = AMOUNT*2 + 1;
impl Solution {
    pub fn sort_array(nums: Vec<i32>) -> Vec<i32> {
        return Self::counting_sort(&nums)
    }

    fn counting_sort(nums: &Vec<i32>) -> Vec<i32> {
        let mut counter: [usize; AMOUNT_LENGTH] = [0; AMOUNT_LENGTH];
        for &num in nums {
            counter[num as usize +AMOUNT] += 1;
        }

        let mut prefix_sum: [usize; AMOUNT_LENGTH] = [0; AMOUNT_LENGTH];
        for index in 0..(AMOUNT_LENGTH) {
            prefix_sum[index] = counter[index];
            if index > 0 {
                prefix_sum[index] += prefix_sum[index-1];
            }
        }

        let n: usize = nums.len();
        let mut result: Vec<i32> = Vec::with_capacity(n);
        for _ in 0..n {
            result.push(0);
        }
        for &num in nums {
            prefix_sum[num as usize+AMOUNT] -= 1;
            result[prefix_sum[num as usize+AMOUNT]] = num;
        }

        return result
    }
}
```

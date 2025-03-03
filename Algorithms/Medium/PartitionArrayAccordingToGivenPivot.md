![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 2161. [Partition Array According To Given Pivot](https://leetcode.com/problems/partition-array-according-to-given-pivot)

### Solution :

Method 1 (Counter, Time Complexity: $O(N)$, Space Complexity: $O(1)$ (N: the number of elements in `nums`)) :
```rust
impl Solution {
    pub fn pivot_array(nums: Vec<i32>, pivot: i32) -> Vec<i32> {
        let n: usize = nums.len();
        let mut amount_less_than: usize = 0;
        let mut amount_larger_than: usize = 0;
        for &num in &nums {
            if num == pivot {
                continue;
            }

            if num < pivot {
                amount_less_than += 1;
                continue;
            }
            amount_larger_than += 1;
        }

        let mut result: Vec<i32> = vec![pivot; n];
        let mut index_less_than: usize = 0;
        let mut index_larger_than: usize = n - amount_larger_than;
        for &num in &nums {
            if num == pivot {
                continue;
            }

            if num < pivot {
                result[index_less_than] = num;
                index_less_than += 1;
                continue;
            }
            result[index_larger_than] = num;
            index_larger_than += 1;
        }

        return result
    }
}
```

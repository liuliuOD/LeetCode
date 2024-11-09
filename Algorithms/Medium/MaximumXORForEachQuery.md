![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 1829. [Maximum XOR For Each Query](https://leetcode.com/problems/maximum-xor-for-each-query)

### Solution :

Method 1 (Bitwise, Time Complexity: $O(M*N)$, Space Complexity: $O(1)$ (M: the value of `maximum_bit`, N: the number of the elements in `nums`)) :
```rust
impl Solution {
    pub fn get_maximum_xor(nums: Vec<i32>, maximum_bit: i32) -> Vec<i32> {
        let n: usize = nums.len();
        let mut xor: i32 = nums.iter().fold(0, |a, b| a^b);
        let mut result: Vec<i32> = vec![0; n];
        for index in 0..n {
            /* Option 1 */
            for bit in 0..maximum_bit {
                if xor & (1<<bit) != 0 {
                    continue;
                }

                result[index] |= 1 << bit;
            }
            /* Option 2

            let maximum: i32 = (1<<maximum_bit) - 1;
            result[index] = xor ^ maximum;
            */
            xor ^= nums[n-index-1];
        }

        return result
    }
}
```

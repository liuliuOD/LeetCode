![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 2220. [Minimum Bit Flips To Convert Number](https://leetcode.com/problems/minimum-bit-flips-to-convert-number)

### Solution :

Method 1 (Bit, Time Complexity: $O(1)$, Space Complexity: $O(1)$) :
```rust
impl Solution {
    pub fn min_bit_flips(start: i32, goal: i32) -> i32 {
        let or: i32 = start | goal;
        let and: i32 = start & goal;
        return (i32::count_ones(or) - i32::count_ones(and)) as i32
    }
}
```

Method 2 (Bit, Time Complexity: $O(1)$, Space Complexity: $O(1)$) :
```rust
impl Solution {
    pub fn min_bit_flips(start: i32, goal: i32) -> i32 {
        /* Option 1 */
        return i32::count_ones(start^goal) as i32
        /* Option 2

        return (start^goal).count_ones() as i32
        */
    }
}
```

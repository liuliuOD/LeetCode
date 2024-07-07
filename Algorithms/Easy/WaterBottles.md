![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 1518. [Water Bottles](https://leetcode.com/problems/water-bottles)

### Solution :

Method 1 (Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```Rust
impl Solution {
    pub fn num_water_bottles(num_bottles: i32, num_exchange: i32) -> i32 {
        let mut result: i32 = 0;
        let mut remaining: i32 = num_bottles;
        while remaining / num_exchange > 0 {
            result += remaining / num_exchange * num_exchange;
            remaining = remaining%num_exchange + remaining/num_exchange;
        }

        return result + remaining
    }
}
```

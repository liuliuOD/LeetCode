![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 2683. [Neighboring Bitwise XOR](https://leetcode.com/problems/neighboring-bitwise-xor)

### Solution :

[Method 1 (Math Proof) :](https://leetcode.com/problems/neighboring-bitwise-xor/solutions/3521882/c-java-python-explanation-with-formal-proof-one-liner-time-o-n/?orderBy=hot)
```rust
impl Solution {
    pub fn does_valid_array_exist(derived: Vec<i32>) -> bool {
        let mut xor = 0;
        for num in derived.iter() {
            xor ^= num;
        }
        xor == 0
    }
}
```

Method 2 (XOR, Time Complexity: $O(N)$, Space Complexity: $O(1)$ (N: the number of the elements in `derived`)) :
```rust
impl Solution {
    pub fn does_valid_array_exist(derived: Vec<i32>) -> bool {
        let n: usize = derived.len();
        if n == 1 {
            return derived[0] == 0
        }

        let mut current: bool = true;
        for index in 0..n {
            if index < n-1 {
                if derived[index] == 1 {
                    current = !current;
                }

                continue;
            }

            return (derived[n-1] == 1 && !current) || (derived[n-1] == 0 && current)
        }

        unreachable![];
    }
}
```

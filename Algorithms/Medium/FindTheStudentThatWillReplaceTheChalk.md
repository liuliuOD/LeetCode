![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 1894. [Find The Student That Will Replace The Chalk](https://leetcode.com/problems/find-the-student-that-will-replace-the-chalk)

### Solution :

Method 1 (Simulation, ERROR: "Time Limit Exceeded", 71/72) :
```rust
impl Solution {
    pub fn chalk_replacer(chalk: Vec<i32>, mut k: i32) -> i32 {
        let n: usize = chalk.len();
        let mut index: usize = 0;
        while k >= chalk[index] {
            k -= chalk[index];
            index = (index+1) % n;
        }

        return index as i32
    }
}
```

Method 2 (Time Complexity: $O(N)$, Space Complexity: $O(1)$ (N: the number of the elements in `chalk`)) :
```rust
impl Solution {
    pub fn chalk_replacer(chalk: Vec<i32>, mut k: i32) -> i32 {
        let n: usize = chalk.len();
        let amount_of_one_loop: i64 = chalk.iter().map(|value| *value as i64).sum();
        k = ((k as i64) % amount_of_one_loop) as i32;
        let mut index: usize = 0;
        while k >= chalk[index] {
            k -= chalk[index];
            index += 1;
        }

        return index as i32
    }
}
```

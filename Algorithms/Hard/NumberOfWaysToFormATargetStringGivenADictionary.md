![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 1639. [Number Of Ways To Form A Target String Given A Dictionary](https://leetcode.com/problems/number-of-ways-to-form-a-target-string-given-a-dictionary)

### Solution :

Method 1 (DFS + Memoization, Time Complexity: $O(M*N+M*P)$, Space Complexity: $O(M*N)$ (M: the length of `words[0]`, N: the length of `target`, P: the number of the elements in `words`)) :
```rust
const BASE: usize = b'a' as usize;
const MODULO: i64 = 1_000_000_007;
impl Solution {
    pub fn num_ways(words: Vec<String>, target: String) -> i32 {
        let m: usize = words[0].len();
        let mut counter: Vec<Vec<i32>> = vec![vec![0; 26]; m];
        for word in &words {
            for (index, ascii) in word.bytes().enumerate() {
                counter[index][ascii as usize - BASE] += 1;
            }
        }

        let n: usize = target.len();
        let mut memoization: Vec<Vec<i32>> = vec![vec![-1; n]; m];
        return Self::dfs(0, 0, &mut memoization, &counter, target.as_bytes())
    }

    fn dfs(index_counter: usize, index_target: usize, memoization: &mut Vec<Vec<i32>>, counter: &Vec<Vec<i32>>, target: &[u8]) -> i32 {
        if index_target >= target.len() {
            return 1
        }

        if (index_counter >= counter.len()) || ((counter.len()-index_counter) < (target.len()-index_target)) {
            return 0
        }

        if memoization[index_counter][index_target] != -1 {
            return memoization[index_counter][index_target]
        }

        let offset_current: usize = target[index_target] as usize - BASE;
        let mut amount_ways: i64 = Self::dfs(index_counter+1, index_target, memoization, counter, target) as i64;
        amount_ways += counter[index_counter][offset_current] as i64 * Self::dfs(index_counter+1, index_target+1, memoization, counter, target) as i64;
        memoization[index_counter][index_target] = (amount_ways % MODULO) as i32;
        return memoization[index_counter][index_target]
    }
}
```

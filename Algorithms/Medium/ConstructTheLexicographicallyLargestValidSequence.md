![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 1718. [Construct The Lexicographically Largest Valid Sequence](https://leetcode.com/problems/construct-the-lexicographically-largest-valid-sequence)

### Constraints :
```text
1 <= n <= 20
```

### Solution :

Method 1 (Backtracking, Time Complexity: $O(N!)$, Space Complexity: $O(N)$ (N: the value of `n`)) :
```rust
impl Solution {
    pub fn construct_distanced_sequence(n: i32) -> Vec<i32> {
        let mut result: Vec<i32> = vec![0; (2 * n as usize) - 1];
        let mut visited: Vec<bool> = vec![false; 1 + n as usize];
        Self::backtracking(n as usize, 0, &mut result, &mut visited);
        return result
    }

    fn backtracking(n: usize, index: usize, result: &mut Vec<i32>, visited: &mut Vec<bool>) -> bool {
        if result.len() <= index {
            return true
        }

        if result[index] != 0 {
            return Self::backtracking(n, index+1, result, visited)
        }

        result[index] = n as i32;

        for n_next in (1..=n).rev() {
            if visited[n_next] {
                continue;
            }
            visited[n_next] = true;
            result[index] = n_next as i32;

            if n_next == 1 && Self::backtracking(n, index+1, result, visited) {
                return true
            } else if (index+n_next < result.len()) && result[index+n_next] == 0 {
                result[index+n_next] = n_next as i32;
                visited[n_next] = true;
                if Self::backtracking(n, index+1, result, visited) {
                    return true
                }

                result[index+n_next] = 0;
            }

            result[index] = 0;
            visited[n_next] = false;
        }

        return false
    }
}
```

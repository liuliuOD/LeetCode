![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 1980. [Find Unique Binary String](https://leetcode.com/problems/find-unique-binary-string)

### Solution :

Method 1 (Backtracking, Time Complexity: $O(2^N)$, Space Complexity: $O(N)$ (N: the number of elements in `nums`)) :
```rust
use std::collections::HashSet;

impl Solution {
    pub fn find_different_binary_string(nums: Vec<String>) -> String {
        let visited: HashSet<String> = HashSet::from_iter(nums.clone().into_iter());
        let mut result: String = String::new();
        Self::backtracking(&mut result, &visited, &nums);
        return result
    }

    fn backtracking(result: &mut String, visited: &HashSet<String>, nums: &Vec<String>) -> bool {
        let n: usize = visited.len();
        if result.len() == n {
            return !visited.contains(result)
        }

        /* Option 1 */
        result.push('0');
        if Self::backtracking(result, visited, nums) {
            return true
        }
        result.pop();

        result.push('1');
        if Self::backtracking(result, visited, nums) {
            return true
        }
        result.pop();
        /* Option 2

        for ch in ['0', '1'] {
            result.push(ch);
            if Self::backtracking(result, visited, nums) {
                return true
            }

            result.pop();
        }
        */

        return false
    }
}
```

Method 2 (Cantor's Diagonal Argument, Time Complexity: $O(N^2)$, Space Complexity: $O(1)$ (N: the number of elements in `nums`)) :
```rust
impl Solution {
    pub fn find_different_binary_string(nums: Vec<String>) -> String {
        let mut result: String = String::new();
        for index in 0..nums.len() {
            let num: Vec<char> = nums[index].chars().collect::<Vec<char>>();
            result.push(match num[index] {
                '0' => '1',
                _ => '0',
            });
        }

        return result
    }
}
```

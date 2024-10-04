![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 2491. [Divide Players Into Teams Of Equal Skill](https://leetcode.com/problems/divide-players-into-teams-of-equal-skill)

### Solution :

Method 1 (Two Pointer, Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$ (N: the number of the elements in `skills`)) :
```rust
impl Solution {
    pub fn divide_players(mut skill: Vec<i32>) -> i64 {
        skill.sort();

        let mut index_left: usize = 0;
        let mut index_right: usize = skill.len() - 1;
        let mut result: i64 = (skill[index_left] * skill[index_right]) as i64;
        let default_value: i32 = skill[index_left] + skill[index_right];
        while index_left < index_right-1 {
            index_left += 1;
            index_right -= 1;
            if skill[index_left]+skill[index_right] != default_value {
                return -1
            }

            result += (skill[index_left] * skill[index_right]) as i64;
        }

        return result
    }
}
```

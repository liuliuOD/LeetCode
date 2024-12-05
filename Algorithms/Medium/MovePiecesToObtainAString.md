![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 2337. [Move Pieces To Obtain A String](https://leetcode.com/problems/move-pieces-to-obtain-a-string)

### Solution :

Method 1 (Time Complexity: $O(M+N)$, Space Complexity: $O(M+N)$ (M: the number of the elements in `start`, N: the number of the elements in `target`)) :
```rust
impl Solution {
    pub fn can_change(start: String, target: String) -> bool {
        if start.chars().filter(|&character| character != '_').collect::<Vec<char>>() != target.chars().filter(|&character| character != '_').collect::<Vec<char>>() {
            return false
        }

        let mut mapping: [Vec<usize>; 2] = [Vec::new(), Vec::new()];
        for (index, character) in start.chars().enumerate() {
            match character {
                'L' => mapping[0].push(index),
                'R' => mapping[1].push(index),
                '_' | _ => continue,
            }
        }
        mapping[0].reverse();
        mapping[1].reverse();

        for (index, character) in target.chars().enumerate() {
            match character {
                'L' => {
                    if mapping[0].len() == 0 || *mapping[0].last().unwrap() < index {
                        return false
                    }

                    mapping[0].pop();
                },
                'R' => {
                    if mapping[1].len() == 0 || *mapping[1].last().unwrap() > index {
                        return false
                    }

                    mapping[1].pop();
                },
                '_' | _ => continue,
            }
        }

        return true
    }
}
```

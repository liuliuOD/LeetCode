![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 773. [Sliding Puzzle](https://leetcode.com/problems/sliding-puzzle)

### Solution :

Method 1 (DFS, Time Complexity: $O(1)$, Space Complexity: $O(1)$) :
```rust
use std::collections::HashMap;

const SWAP: [[usize; 3]; 6] = [
    [1, 3, 3],
    [0, 2, 4],
    [1, 5, 5],
    [0, 4, 4],
    [1, 3, 5],
    [2, 4, 4],
];
impl Solution {
    pub fn sliding_puzzle(board: Vec<Vec<i32>>) -> i32 {
        let mut counter: HashMap<String, i32> = HashMap::new();
        let mut states: Vec<u8> = Vec::with_capacity(6);
        let mut index_zero: usize = 0;
        for (index_m, row) in board.iter().enumerate() {
            for (index_n, &element) in row.iter().enumerate() {
                states.push(element as u8);

                if element == 0 {
                    index_zero = index_m*3 + index_n;
                }
            }
        }
        Self::dfs(index_zero, 0, &mut states, &mut counter);

        return match counter.get("123450") {
            Some(result) => *result,
            None => -1,
        }
    }

    fn dfs(index_zero: usize, amount_move: i32, states: &mut Vec<u8>, counter: &mut HashMap<String, i32>) {
        let key: String = Self::get_key(states);
        if counter.contains_key(&key) && *counter.get(&key).unwrap() <= amount_move {
            return
        }
        counter.entry(key).and_modify(|value| *value = amount_move).or_insert(amount_move);

        for &index_swap in SWAP[index_zero].iter() {
            states.swap(index_zero, index_swap);
            Self::dfs(index_swap, amount_move+1, states, counter);
            states.swap(index_swap, index_zero);
        }
    }

    fn get_key(states: &Vec<u8>) -> String {
        let mut key: String = String::new();
        for &state in states.iter() {
            key.push_str(&String::from_utf8(Vec::from([b'0' + state])).unwrap());
        }

        return key.to_string()
    }
}
```

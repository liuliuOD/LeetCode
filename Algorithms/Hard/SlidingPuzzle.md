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

Method 2 (BFS, Time Complexity: $O(1)$, Space Complexity: $O(1)$) :
```rust
use std::collections::{HashSet, VecDeque};

const TARGET: &str = "123450";
const BASE: u8 = b'0';
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

        return Self::bfs(index_zero, &mut states)
    }

    fn bfs(index_zero: usize, states: &mut Vec<u8>) -> i32 {
        let key_start: String = Self::get_key(states);
        let mut visited: HashSet<String> = HashSet::from([key_start.clone()]);
        let mut queue: VecDeque<(String, usize, i32)> = VecDeque::from([(key_start, index_zero, 0)]);
        while queue.len() > 0 {
            let current = queue.pop_front().unwrap();
            if current.0 == TARGET.to_string() {
                return current.2
            }

            visited.insert(current.0.clone());

            let mut current_states: Vec<u8> = current.0.bytes().map(|ascii| ascii - BASE).collect();
            for &index_swap in SWAP[current.1].iter() {
                current_states.swap(current.1, index_swap);
                let key_next: String = Self::get_key(&current_states);
                current_states.swap(index_swap, current.1);
                if visited.contains(&key_next) {
                    continue;
                }

                queue.push_back((key_next, index_swap, current.2+1));
            }
        }

        return -1
    }

    fn get_key(states: &Vec<u8>) -> String {
        let mut key: String = String::new();
        for &state in states.iter() {
            key.push((BASE + state) as char);
        }

        return key.to_string()
    }
}
```

Method 3 (BFS, Time Complexity: $O(1)$, Space Complexity: $O(1)$) :
```rust
use std::collections::{HashSet, VecDeque};

const TARGET: &str = "123450";
const BASE: u8 = b'0';
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

        return Self::bfs(index_zero, &mut states)
    }

    fn bfs(index_zero: usize, states: &mut Vec<u8>) -> i32 {
        let key_start: String = Self::get_key(states);
        let mut visited: HashSet<String> = HashSet::from([key_start.clone()]);
        let mut queue: VecDeque<(String, usize)> = VecDeque::from([(key_start, index_zero)]);
        let mut result: i32 = 0;
        while queue.len() > 0 {
            for _ in 0..queue.len() {
                let current: (String, usize) = queue.pop_front().unwrap();
                if current.0 == TARGET.to_string() {
                    return result
                }

                visited.insert(current.0.clone());

                let mut current_states: Vec<u8> = current.0.bytes().map(|ascii| ascii - BASE).collect();
                for &index_swap in SWAP[current.1].iter() {
                    current_states.swap(current.1, index_swap);
                    let key_next: String = Self::get_key(&current_states);
                    current_states.swap(index_swap, current.1);
                    if visited.contains(&key_next) {
                        continue;
                    }

                    queue.push_back((key_next, index_swap));
                }
            }

            result += 1;
        }

        return -1
    }

    fn get_key(states: &Vec<u8>) -> String {
        let mut key: String = String::new();
        for &state in states.iter() {
            key.push((BASE + state) as char);
        }

        return key.to_string()
    }
}
```

Method 4 (BFS + Optimization, Time Complexity: $O(1)$, Space Complexity: $O(1)$) :
```rust
use std::collections::{HashSet, VecDeque};

const TARGET: &str = "123450";
const BASE: u8 = b'0';
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
        let mut states: Vec<u8> = Vec::with_capacity(6);
        for (index_m, row) in board.iter().enumerate() {
            for (index_n, &element) in row.iter().enumerate() {
                states.push(element as u8);
            }
        }

        return Self::bfs(&mut states)
    }

    fn bfs(states: &mut Vec<u8>) -> i32 {
        let key_start: String = Self::get_key(states);
        let mut visited: HashSet<String> = HashSet::from([key_start.clone()]);
        let mut queue: VecDeque<String> = VecDeque::from([key_start]);
        let mut result: i32 = 0;
        while queue.len() > 0 {
            for _ in 0..queue.len() {
                let current: String = queue.pop_front().unwrap();
                if current == TARGET.to_string() {
                    return result
                }

                visited.insert(current.clone());

                let mut current_states: Vec<u8> = current.bytes().map(|ascii| ascii - BASE).collect();
                let index_current_zero: usize = current.find('0').unwrap();
                for &index_swap in SWAP[index_current_zero].iter() {
                    current_states.swap(index_current_zero, index_swap);
                    let key_next: String = Self::get_key(&current_states);
                    current_states.swap(index_swap, index_current_zero);
                    if visited.contains(&key_next) {
                        continue;
                    }

                    queue.push_back(key_next);
                }
            }

            result += 1;
        }

        return -1
    }

    fn get_key(states: &Vec<u8>) -> String {
        let mut key: String = String::new();
        for &state in states.iter() {
            key.push((BASE + state) as char);
        }

        return key.to_string()
    }
}
```

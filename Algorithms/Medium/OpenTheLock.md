![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
![language-Go](https://img.shields.io/badge/Go-00add8?style=for-the-badge&logo=GO&logoColor=white)
---

## 752. [Open The Lock](https://leetcode.com/problems/open-the-lock)

### Solution :

Method 1 (BFS, Time Complexity: $O(4*(N+10^4))$ (N: length of `deadends`), Space Complexity: $O(4*(N+10^4))$) :
```rust
use std::collections::{HashSet, VecDeque};

impl Solution {
    pub fn open_lock(deadends: Vec<String>, target: String) -> i32 {
        let BASE: String = String::from("0000");
        let mut visited: HashSet<String> = HashSet::from_iter(deadends);
        if visited.contains(&BASE) {
            return -1
        }

        let mut queue: VecDeque<String> = VecDeque::from([BASE]);
        let mut result: i32 = 0;
        while queue.len() > 0 {
            let n: usize = queue.len();
            for _ in 0..n {
                let current = queue.pop_front().unwrap();
                if visited.contains(&current) {
                    continue;
                }
                if current == target {
                    return result
                }
                visited.insert(current.clone());

                for index_slot in 0..4 {
                    let mut current_temp: String = current.clone();
                    let current_char: char = current_temp.chars().nth(index_slot).unwrap();
                    // next
                    current_temp.replace_range(index_slot..index_slot+1, &Self::move_next(current_char));
                    queue.push_back(current_temp.clone());
                    // previous
                    current_temp.replace_range(index_slot..index_slot+1, &Self::move_previous(current_char));
                    queue.push_back(current_temp);
                }
            }

            result += 1;
        }

        return -1
    }

    fn move_next(slot: char) -> String {
        if slot < '9' {
            return char::from_u32(slot as u32 + 1).unwrap().to_string()
        }
        return "0".to_string()
    }

    fn move_previous(slot: char) -> String {
        if slot > '0' {
            return char::from_u32(slot as u32 - 1).unwrap().to_string()
        }
        return "9".to_string()
    }
}
```

### Solution :

Method 1 (BFS, Time Complexity: $O(4*(N+10^4))$ (N: length of `deadends`), Space Complexity: $O(4*(N+10^4))$) :
```python
SLOT_MOVES: List[Dict[str, str]] = [
    # NEXT
    {
        "0": "1",
        "1": "2",
        "2": "3",
        "3": "4",
        "4": "5",
        "5": "6",
        "6": "7",
        "7": "8",
        "8": "9",
        "9": "0",
    },
    # PREVIOUS
    {
        "1": "0",
        "2": "1",
        "3": "2",
        "4": "3",
        "5": "4",
        "6": "5",
        "7": "6",
        "8": "7",
        "9": "8",
        "0": "9",
    }
]
BASE: str = "0000"

class Solution:
    def openLock(self, deadends: List[str], target: str) -> int:
        visited = set(deadends)
        result: int = -1
        if BASE in visited:
            return result

        visited.add(BASE)
        queue = deque([BASE])
        while queue:
            result += 1

            amount = len(queue)
            for _ in range(amount):
                current = queue.popleft()
                print(current)
                if current == target:
                    return result

                for index_slot in range(4):
                    for index_direction in range(2):
                        current_list = list(current)
                        current_list[index_slot] = SLOT_MOVES[index_direction][current_list[index_slot]]

                        next_lock = ''.join(current_list)
                        if next_lock in visited:
                            continue
                        visited.add(next_lock)
                        queue.append(next_lock)

        # can't open the lock
        return -1
```

### Solution :

Method 1 (BFS, Time Complexity: $O(4*(N+10^4))$ (N: length of `deadends`), Space Complexity: $O(4*(N+10^4))$) :
```go
import "container/list"

const BASE string = "0000"
func openLock(deadends []string, target string) int {
    var visited map[string]bool = make(map[string]bool)
    for _, item := range deadends {
        visited[item] = true
    }

    _, ok := visited[BASE]
    if ok {
        return -1
    }

    queue := list.New()
    queue.PushBack(BASE)
    visited[BASE] = true
    for result := 0; queue.Len() > 0; result++ {
        amount := queue.Len()
        for index := 0; index < amount; index++ {
            current := queue.Front()
            queue.Remove(current)
            current_val := current.Value.(string)
            if current_val == target {
                return result
            }

            for index_slot := 0; index_slot < 4; index_slot++ {
                current_next := current_val
                current_next = current_next[:index_slot] + move_next(current_next[index_slot]) + current_next[index_slot+1:]
                _, ok := visited[current_next]
                if !ok {
                    queue.PushBack(current_next)
                }
                visited[current_next] = true

                current_previous := current_val
                current_previous = current_previous[:index_slot] + move_previous(current_previous[index_slot]) + current_previous[index_slot+1:]
                _, ok = visited[current_previous]
                if !ok {
                    queue.PushBack(current_previous)
                }
                visited[current_previous] = true
            }
        }
    }

    return -1
}

func move_next(current byte) string {
    if current + 1 <= '9' {
        return string(current + 1)
    }
    return "0"
}
func move_previous(current byte) string {
    if current - 1 >= '0' {
        return string(current - 1)
    }
    return "9"
}
```

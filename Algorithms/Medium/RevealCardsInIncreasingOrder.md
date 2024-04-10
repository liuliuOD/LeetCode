![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 950. [Reveal Cards In Increasing Order](https://leetcode.com/problems/reveal-cards-in-increasing-order)

### Solution :

Method 1 (Double-ended Queue, Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$) :
```rust
use std::collections::VecDeque;

impl Solution {
    pub fn deck_revealed_increasing(mut deck: Vec<i32>) -> Vec<i32> {
        let mut result: VecDeque<i32> = VecDeque::new();
        deck.sort();
        deck.reverse();
        for num in deck {
            if result.len() >= 2 {
                let latest: i32 = result.pop_back().unwrap();
                result.push_front(latest);
            }

            result.push_front(num);
        }

        return result.into_iter().collect::<Vec<i32>>()
    }
}
```

Method 2 (Double-ended Queue, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```rust
use std::collections::VecDeque;

const MAX_VALUE: usize = 1_000_001;
impl Solution {
    pub fn deck_revealed_increasing(deck: Vec<i32>) -> Vec<i32> {
        let mut result: VecDeque<i32> = VecDeque::new();
        let mut sorted: [bool; MAX_VALUE] = [false; 1_000_001];
        for num in deck {
            sorted[num as usize] = true;
        }

        for num in (1..MAX_VALUE).rev() {
            if sorted[num] == false {
                continue
            }

            if result.len() >= 2 {
                let latest: i32 = result.pop_back().unwrap();
                result.push_front(latest);
            }

            result.push_front(num as i32);
        }

        return result.into_iter().collect::<Vec<i32>>()
    }
}
```

### Solution :

Method 1 (Brute Force, Time Complexity: $O(N^2)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def deckRevealedIncreasing(self, deck: List[int]) -> List[int]:
        result = []
        deck.sort(reverse=True)
        for num in deck:
            if len(result) >= 2:
                result = result[-1:] + result[:-1]

            result = [num] + result

        return result
```

Method 2 (Double-ended Queue, Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$) :
```python
class Solution:
    def deckRevealedIncreasing(self, deck: List[int]) -> List[int]:
        result = deque()
        deck.sort(reverse=True)
        for num in deck:
            if len(result) >= 2:
                result.appendleft(result.pop())

            result.appendleft(num)

        return result
```

![language-RUST](https://img.shields.io/badge/%20-RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2147. [Number Of Ways To Divide A Long Corridor](https://leetcode.com/problems/number-of-ways-to-divide-a-long-corridor)

### Solution :

Method 1 :
```rust
const MODULO: i64 = 1_000_000_007;

impl Solution {
    pub fn number_of_ways(corridor: String) -> i32 {
        let mut seats: Vec<i32> = vec![];
        for (index, ascii) in corridor.bytes().enumerate() {
            if ascii == 83 {
                seats.push(index as i32);
            }
        }

        if seats.len() % 2 == 1 || seats.len() == 0 {
            return 0
        }

        let mut result: i64 = 1;
        seats[1..seats.len()-1].chunks(2).for_each(|window| {
            result = result * (window[1]-window[0]) as i64 % MODULO;
        });
        return result as _
    }
}
```

Metho 2 (Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```rust
const MODULO: i64 = 1_000_000_007;

impl Solution {
    pub fn number_of_ways(corridor: String) -> i32 {
        let mut amount_seat: i32 = 0;
        let mut result: i64 = 1;
        let mut index_previous: usize = 0;
        for (index, ascii) in corridor.bytes().enumerate() {
            if ascii == 83 {
                amount_seat += 1;
                if amount_seat == 1 {
                    continue;
                }

                if amount_seat % 2 == 0 {
                    index_previous = index;
                } else {
                    result = result * (index-index_previous) as i64 % MODULO;
                }
            }
        }

        if amount_seat % 2 == 1 || amount_seat == 0 {
            return 0
        }
        return result as _
    }
}
```

### Solution :

Method 1 (Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
MODULO = 1_000_000_007

class Solution:
    def numberOfWays(self, corridor: str) -> int:
        seats = []
        for index, char in enumerate(corridor):
            if char == "P":
                continue

            seats.append(index)

        amount_seat = len(seats)
        if amount_seat % 2 == 1 or amount_seat == 0:
            return 0

        result = 1
        for index in range(2, amount_seat, 2):
            result = (result * (seats[index]-seats[index-1])) % MODULO

        return result
```

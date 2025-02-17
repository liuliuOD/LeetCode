![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 1079. [Letter Tile Possibilities](https://leetcode.com/problems/letter-tile-possibilities)

### Solution :

Method 1 (Backtracking, Time Complexity: $O(2^N)$, Space Complexity: $O(N)$ (N: the number of elements in `tiles`)) :
```rust
const BASE: u8 = b'A';

impl Solution {
    pub fn num_tile_possibilities(tiles: String) -> i32 {
        let mut counter: [i32; 26] = [0; 26];
        for ascii in tiles.bytes() {
            counter[(ascii - BASE) as usize] += 1;
        }

        return Self::backtracking(&mut counter)
    }

    fn backtracking(counter: &mut [i32; 26]) -> i32 {
        let mut result: i32 = 0;
        for index_next in 0..26 {
            if counter[index_next] <= 0 {
                continue;
            }
            counter[index_next] -= 1;
            result += 1 + Self::backtracking(counter);
            counter[index_next] += 1;
        }

        return result
    }
}
```

```rust
const BASE: u8 = b'A';
const AMOUNT_CANDIDATE: usize = 26;

impl Solution {
    pub fn num_tile_possibilities(tiles: String) -> i32 {
        let mut counter: [i32; AMOUNT_CANDIDATE] = [0; AMOUNT_CANDIDATE];
        for ascii in tiles.bytes() {
            counter[(ascii - BASE) as usize] += 1;
        }

        return Self::backtracking(&mut counter)
    }

    fn backtracking(counter: &mut [i32; AMOUNT_CANDIDATE]) -> i32 {
        let mut result: i32 = 0;
        for index_next in 0..AMOUNT_CANDIDATE {
            if counter[index_next] <= 0 {
                continue;
            }
            counter[index_next] -= 1;
            result += 1 + Self::backtracking(counter);
            counter[index_next] += 1;
        }

        return result
    }
}
```

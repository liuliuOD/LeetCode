![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 3016. [Minimum Number Of Pushes To Type Word II](https://leetcode.com/problems/minimum-number-of-pushes-to-type-word-ii)

### Solution :

Method 1 (Array + Sort, Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```rust
const BASE: usize = 8;
impl Solution {
    pub fn minimum_pushes(word: String) -> i32 {
        let mut frequency_ordered: [i32; 26] = [0; 26];
        for ch in word.bytes() {
            frequency_ordered[(ch - b'a') as usize] += 1;
        }
        frequency_ordered.sort_unstable_by(|a, b| b.cmp(a));

        let mut result: i32 = 0;
        let mut counter: usize = 0;
        for amount_push in frequency_ordered.into_iter() {
            result += (counter/BASE + 1) as i32 * amount_push;
            counter += 1;
        }

        return result
    }
}
```

### Solution :

Method 1 (Hash Map + Sort, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
BASE = 8
class Solution:
    def minimumPushes(self, word: str) -> int:
        counter = Counter(word)
        mapping = defaultdict(list)
        for char, amount in counter.items():
            mapping[amount].append(char)

        result = 0
        loop = 0
        for amount in sorted(mapping.keys(), reverse=True):
            for _ in mapping[amount]:
                loop += 1
                result += ((loop+7) // BASE) * amount

        return result
```

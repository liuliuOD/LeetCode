![language-RUST](https://img.shields.io/badge/%20-RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2953. [Count Complete Substrings](https://leetcode.com/problems/count-complete-substrings)

### Solution :

Method 1 :
```rust
const BASE: u8 = b'a';

impl Solution {
    pub fn count_complete_substrings(word: String, k: i32) -> i32 {
        let word_bytes: Vec<u8> = word.bytes().collect();
        let n: usize = word_bytes.len();
        let mut result: i32 = 0;
        for amount_unique in 1..=26 {
            let window: usize = amount_unique * k as usize;
            if window > n {
                break;
            }

            let mut counter: [i32; 26] = [0; 26];
            let mut left: usize = 0;
            for right in 0..n {
                if right > 0 && (word_bytes[right] as i32-word_bytes[right-1] as i32).abs() > 2 {
                    counter = [0; 26];
                    left = right;
                }

                counter[(word_bytes[right]-BASE) as usize] += 1;
                if (right-left+1) > window {
                    counter[(word_bytes[left]-BASE) as usize] -= 1;
                    left += 1;
                }

                if (right-left+1) == window && Self::is_complete(k, &counter) {
                    result += 1;
                }
            }
        }

        return result
    }

    fn is_complete(k: i32, counter: &[i32; 26]) -> bool {
        for index in 0..26 {
            if counter[index] != 0 && counter[index] != k {
                return false
            }
        }

        return true
    }
}
```

### Solution :

Method 1 :
```python
class Solution:
    def countCompleteSubstrings(self, word: str, k: int) -> int:
        n = len(word)
        result = 0
        for amount_unique in range(1, 27):
            window = amount_unique * k
            if window > n:
                break

            counter = defaultdict(int)
            left = 0
            for right in range(n):
                if right > 0 and abs(ord(word[right])-ord(word[right-1])) > 2:
                    left = right
                    counter = defaultdict(int)

                counter[word[right]] += 1
                if (right-left+1) > window:
                    counter[word[left]] -= 1
                    left += 1

                if (right-left+1) == window and self.isComplete(k, counter):
                    result += 1

        return result

    def isComplete(self, k: int, counter: Dict[str, int]) -> bool:
        for frequency in counter.values():
            if frequency > 0 and frequency != k:
                return False

        return True
```

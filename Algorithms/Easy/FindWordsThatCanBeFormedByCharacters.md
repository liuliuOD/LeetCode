![language-RUST](https://img.shields.io/badge/%20-RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1160. [Find Words That Can Be Formed By Characters](https://leetcode.com/problems/find-words-that-can-be-formed-by-characters)

### Solution :

Method 1 (Time Complexity: $O(M+P*N)$ (M: length of `chars`, P: amount of `words`, N: the maximum length of word in `words`), Space Complexity: $O(1)$) :
```rust
impl Solution {
    pub fn count_characters(words: Vec<String>, chars: String) -> i32 {
        let mut mapping: [i32; 26] = [0; 26];
        let base: usize = 'a' as _;
        for ch in chars.chars() {
            mapping[ch as usize - base] += 1;
        }

        let mut result: i32 = 0;
        for word in words {
            let mut mapping_word: [i32; 26] = [0; 26];
            for ch in word.chars() {
                mapping_word[ch as usize - base] += 1;
            }

            let mut is_good: bool = true;
            for index in 0..26 {
                if mapping_word[index] > mapping[index] {
                    is_good = false;
                    break;
                }
            }

            /* Option 1 */
            if is_good {
                result += word.len() as i32;
            }
            /* Option 2

            if !is_good {
                continue;
            }

            result += word.len() as i32;
            */
        }

        return result
    }
}
```

### Solution :

Method 1 :
```python
class Solution:
    def countCharacters(self, words: List[str], chars: str) -> int:
        mapping = Counter(chars)
        result = 0
        for word in words:
            is_good = True
            counter = Counter(word)
            for key in counter:
                if key not in mapping or mapping[key] < counter[key]:
                    is_good = False
                    break

            if is_good:
                result += len(word)

        return result
```

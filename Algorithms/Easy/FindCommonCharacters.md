![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1002. [Find Common Characters](https://leetcode.com/problems/find-common-characters)

### Solution :

Method 1 (Time Complexity: $O(M*N)$ (M: average length of elements in `words`, N: length of `words`), Space Complexity: $O(1)$) :
```rust
const BASE: usize = 'a' as usize;

impl Solution {
    pub fn common_chars(words: Vec<String>) -> Vec<String> {
        let mut frequency: [usize; 26] = [usize::MAX; 26];
        for word in words {
            let mut frequency_current: [usize; 26] = [0; 26];
            for ascii in word.bytes() {
                frequency_current[ascii as usize - BASE] += 1;
            }

            for index in 0..26 {
                frequency[index] = std::cmp::min(frequency[index], frequency_current[index]);
            }
        }

        let mut result: Vec<String> = vec![];
        for index in 0..26 {
            while frequency[index] > 0 {
                result.push(((BASE+index) as u8 as char).to_string());
                frequency[index] -= 1;
            }
        }

        return result
    }
}
```

### Solution :

Method 1 (Time Complexity: $O(M*N)$ (M: average length of elements in `words`, N: length of `words`), Space Complexity: $O(N)$) :
```python
class Solution:
    def commonChars(self, words: List[str]) -> List[str]:
        n = len(words)
        frequency = [Counter(word) for word in words]
        result = []
        for char in frequency[0].keys():
            amount_minimum = inf
            for index in range(n):
                if char not in frequency[index]:
                    break

                amount_minimum = min(amount_minimum, frequency[index][char])
            else:
                result.extend([char] * amount_minimum)

        return result
```

Method 2 (Time Complexity: $O(M*N)$ (M: average length of elements in `words`, N: length of `words`), Space Complexity: $O(1)$) :
```python
BASE = ord("a")
class Solution:
    def commonChars(self, words: List[str]) -> List[str]:
        n = len(words)
        frequency = [inf] * 26
        for word in words:
            counter = Counter(word)
            for offset in range(26):
                char = chr(BASE + offset)
                frequency[offset] = min(frequency[offset], counter.get(char, 0))

        result = []
        for offset, amount in enumerate(frequency):
            result += [chr(BASE+offset)] * amount
        return result
```

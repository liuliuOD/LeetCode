![language-RUST](https://img.shields.io/badge/%20-RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2785. [Sort Vowels In A String](https://leetcode.com/problems/sort-vowels-in-a-string)

### Solution :

Method 1 :
```rust
impl Solution {
    pub fn sort_vowels(s: String) -> String {
        let WHITE_LIST: [char; 10] = ['a', 'e', 'i', 'o', 'u', 'A', 'E', 'I', 'O', 'U',];
        let mut vowels: Vec<String> = vec![];
        let mut positions: Vec<usize> = vec![];
        for (index, ch) in s.chars().enumerate() {
            if WHITE_LIST.contains(&ch) {
                vowels.push(ch.to_string());
                positions.push(index);
            }
        }

        vowels.sort();
        let mut result: String = s;
        let mut index_vowel: usize = 0;
        for index in positions {
            result.replace_range(index..index+1, &vowels[index_vowel]);
            index_vowel += 1;
        }

        return result
    }
}
```

### Solution :

Method 1 (Binary Heap, Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$) :
```python
class Solution:
    def sortVowels(self, s: str) -> str:
        index_list = []
        alpha = []
        for index, ch in enumerate(s):
            if ch in ['a', 'e', 'i', 'o', 'u', 'A', 'E', 'I', 'O', 'U']:
                index_list.append(index)
                heapq.heappush(alpha, ch)
        
        result = list(s)
        for index in index_list:
            ch = heapq.heappop(alpha)
            result[index] = ch
        
        return ''.join(result)
```

Method 2 (Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$) :
```python
class Solution:
    def sortVowels(self, s: str) -> str:
        vowels = []
        positions = []
        for index, char in enumerate(s):
            if char not in ['a', 'e', 'i', 'o', 'u', 'A', 'E', 'I', 'O', 'U']:
                continue

            vowels.append(char)
            positions.append(index)

        vowels.sort()
        result = list(s)
        index_vowel = 0
        for index in positions:
            result[index] = vowels[index_vowel]
            index_vowel += 1

        return ''.join(result)
```

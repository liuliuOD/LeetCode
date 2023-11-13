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

Method 2 (Counting Sort) :
```rust
use std::collections::HashMap;

impl Solution {
    pub fn sort_vowels(s: String) -> String {
        let ORDER_LIST: [char; 10] = ['A', 'E', 'I', 'O', 'U', 'a', 'e', 'i', 'o', 'u',];
        let mut vowels: HashMap<char, i32> = HashMap::new();
        for (index, ch) in s.chars().enumerate() {
            if ORDER_LIST.contains(&ch) {
                vowels.entry(ch).and_modify(|item| *item += 1).or_insert(1);
            }
        }

        let mut result: Vec<char> = vec![];
        let mut index_order: usize = 0;
        for ch in s.chars() {
            if ORDER_LIST.contains(&ch) {
                let mut char_update: char = ORDER_LIST[index_order];
                while !vowels.contains_key(&char_update) || vowels[&char_update] == 0 {
                    index_order += 1;
                    char_update = ORDER_LIST[index_order];
                }

                vowels.entry(char_update).and_modify(|item| *item -= 1);
                result.push(char_update);
            } else {
                result.push(ch);
            }
        }

        return result.iter().collect::<String>()
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

Method 3 (Counting Sort, Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def sortVowels(self, s: str) -> str:
        ORDER_VOWEL = ['A', 'E', 'I', 'O', 'U', 'a', 'e', 'i', 'o', 'u']
        vowels = defaultdict(int)
        for index, char in enumerate(s):
            if char not in ORDER_VOWEL:
                continue

            vowels[char] += 1

        result = ''
        index_order = 0
        for index in range(len(s)):
            if s[index] in ORDER_VOWEL:
                char = ORDER_VOWEL[index_order]
                while vowels[char] == 0:
                    index_order += 1
                    char = ORDER_VOWEL[index_order]

                vowels[char] -= 1
                result += char
            else:
                result += s[index]

        return result
```

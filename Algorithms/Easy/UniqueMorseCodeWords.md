![language-RUST](https://img.shields.io/badge/%20-RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 804. [Unique Morse Code Words](https://leetcode.com/problems/unique-morse-code-words)

### Solution :

Method 1 (Set) :
```rust
use std::collections::HashSet;
impl Solution {
    pub fn unique_morse_representations(words: Vec<String>) -> i32 {
        let mapping: [&str; 26] = [".-","-...","-.-.","-..",".","..-.","--.","....","..",".---","-.-",".-..","--","-.","---",".--.","--.-",".-.","...","-","..-","...-",".--","-..-","-.--","--.."];

        return words
            .iter()
            .map(|word| word
                .as_bytes()
                .iter()
                .map(|&byte| mapping[(byte - b'a') as usize])
                .collect::<String>())
            .collect::<HashSet<String>>()
            .len() as _
    }
}
```

Method 2 (Set) :
```rust
use std::collections::HashSet;
const MAPPING: [&str; 26] = [".-","-...","-.-.","-..",".","..-.","--.","....","..",".---","-.-",".-..","--","-.","---",".--.","--.-",".-.","...","-","..-","...-",".--","-..-","-.--","--.."];

impl Solution {
    pub fn unique_morse_representations(words: Vec<String>) -> i32 {
        /* Option 1 */
        return words
            .iter()
            .map(|word| word
                .as_bytes()
                .iter()
                .map(|&byte| MAPPING[(byte - b'a') as usize])
                .collect::<String>())
            .collect::<HashSet<String>>()
            .len() as _
        /* Option 2

        return words
            .iter()
            .map(|word| word
                .bytes()
                .map(|byte| MAPPING[(byte - b'a') as usize])
                .collect::<String>())
            .collect::<HashSet<String>>()
            .len() as _
        */
    }
}
```

### Solution :

Method 1 (Set) :
```python
class Solution:
    def uniqueMorseRepresentations(self, words: List[str]) -> int:
        result = set()
        mapping = [".-","-...","-.-.","-..",".","..-.","--.","....","..",".---","-.-",".-..","--","-.","---",".--.","--.-",".-.","...","-","..-","...-",".--","-..-","-.--","--.."]
        base = ord('a')
        for word in words:
            encoded = ''
            for char in word:
                encoded += mapping[ord(char)-base]

            result.add(encoded)

        return len(result)
```

Method 2 (Bitwise) :
```python
class Solution:
    def uniqueMorseRepresentations(self, words: List[str]) -> int:
        result = set()
        mapping = [0b10, 0b0111, 0b0101, 0b011, 0b1, 0b1101, 0b001, 0b1111, 0b11, 0b1000, 0b010, 0b1011, 0b00, 0b01, 0b000, 0b1001, 0b0010, 0b101, 0b111, 0b0, 0b110, 0b1110, 0b100, 0b0110, 0b0100, 0b0011]
        length = [2, 4, 4, 3, 1, 4, 3, 4, 2, 4, 3, 4, 2, 2, 3, 4, 4, 3, 3, 1, 3, 4, 3, 4, 4, 4]
        base = ord('a')
        for word in words:
            binary = 0b0
            for char in word:
                index = ord(char)-base
                binary = (binary<<length[index]) | mapping[index]

            result.add(binary)

        return len(result)
```

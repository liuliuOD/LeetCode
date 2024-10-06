![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1813. [Sentence Similarity III](https://leetcode.com/problems/sentence-similarity-iii)

### Solution :

Method 1 (Brute Force) :
```rust
const SPACE: u8 = b' ';

impl Solution {
    pub fn are_sentences_similar(mut sentence1: String, mut sentence2: String) -> bool {
        let mut m: usize = sentence1.len();
        let mut n: usize = sentence2.len();
        if m > n {
            std::mem::swap(&mut sentence1, &mut sentence2);
            std::mem::swap(&mut m, &mut n);
        }

        let sentence1_bytes: Vec<u8> = sentence1.as_bytes().to_vec();
        let sentence2_bytes: Vec<u8> = sentence2.as_bytes().to_vec();
        if sentence1 == sentence2 ||
            (sentence2.starts_with(&sentence1) && sentence2_bytes[m] == SPACE) ||
            (sentence2.ends_with(&sentence1) && sentence2_bytes[n-m-1] == SPACE) {
            return true
        }

        for index in 0..m {
            if sentence1_bytes[index] != SPACE {
                continue;
            }

            if (sentence2.starts_with(&String::from_utf8(sentence1_bytes[..index].to_vec()).unwrap()) && sentence2_bytes[index] == SPACE) &&
                (sentence2.ends_with(&String::from_utf8(sentence1_bytes[index..].to_vec()).unwrap()) && sentence2_bytes[n-(m-index)] == SPACE) {
                return true
            }
        }

        return false
    }
}
```

### Solution :

Method 1 (Brute Force) :
```python
class Solution:
    def areSentencesSimilar(self, sentence1: str, sentence2: str) -> bool:
        m, n = len(sentence1), len(sentence2)
        if m > n:
            m, n = n, m
            sentence1, sentence2 = sentence2, sentence1

        if sentence1 == sentence2 or (sentence2.startswith(sentence1) and sentence2[m] == " ") or (sentence2.endswith(sentence1) and sentence2[-m-1] == " "):
            return True

        for index_left in range(m):
            if sentence1[index_left] != " ":
                continue

            if sentence2.startswith(sentence1[:index_left+1]) and sentence2.endswith(sentence1[index_left+1:]) and sentence2[index_left] == " " and sentence2[-(m-index_left)] == " ":
                return True

        return False
```

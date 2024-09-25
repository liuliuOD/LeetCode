![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2416. [Sum Of Prefix Scores Of Strings](https://leetcode.com/problems/sum-of-prefix-scores-of-strings)

### Solution :

Method 1 (Hash Map, Time Complexity: $O(N*K)$, Space Complexity: $O(N*K)$, ERROR: "Time Limit Exceeded" (35/38) (N: the number of the elements in `words`, K: the average length of each element in `words`)) :
```rust
use std::collections::HashMap;

impl Solution {
    pub fn sum_prefix_scores(words: Vec<String>) -> Vec<i32> {
        let mut mapping: HashMap<String, i32> = HashMap::new();
        for word in words.iter() {
            for length in 1..=word.len() {
                mapping.entry(word[0..length].to_string()).and_modify(|value| *value += 1).or_insert(1);
            }
        }

        let mut result: Vec<i32> = Vec::new();
        for word in words.iter() {
            let mut score: i32 = 0;
            for length in 1..=word.len() {
                score += mapping[&word[0..length].to_string()];
            }

            result.push(score);
        }

        return result
    }
}
```

Method 2 (Trie Tree, Time Complexity: $O(N*K)$, Space Complexity: $O(N*K)$ (N: the number of the elements in `words`, K: the average length of each element in `words`)) :
```rust
struct TrieNode {
    children: [Option<Box<TrieNode>>; 26],
    amount: i32,
}

impl TrieNode {
    pub fn new() -> Self {
        return Self {
            children: Default::default(),
            amount: 0,
        }
    }
}

const BASE: u8 = b'a';

impl Solution {
    pub fn sum_prefix_scores(words: Vec<String>) -> Vec<i32> {
        let mut trie: TrieNode = TrieNode::new();
        for word in words.iter() {
            let mut current: &mut TrieNode = &mut trie;
            for ascii in word.as_bytes() {
                let offset: usize = (ascii - BASE) as usize;
                if current.children[offset].is_none() {
                    current.children[offset] = Some(Box::new(TrieNode::new()));
                }

                current.children[offset].as_mut().unwrap().amount += 1;
                current = current.children[offset].as_mut().unwrap();
            }
        }

        let mut result: Vec<i32> = Vec::new();
        for word in words.iter() {
            let mut score: i32 = 0;
            let mut current: &TrieNode = &trie;
            for ascii in word.as_bytes() {
                let offset: usize = (ascii - BASE) as usize;
                score += current.children[offset].as_ref().unwrap().amount;
                current = current.children[offset].as_ref().unwrap();
            }

            result.push(score);
        }

        return result
    }
}
```

### Solution :

Method 1 (Hash Map, Time Complexity: $O(N*K)$, Space Complexity: $O(N*K)$) :
```python
class Solution:
    def sumPrefixScores(self, words: List[str]) -> List[int]:
        mapping = defaultdict(int)
        for word in words:
            for length in range(1, len(word)+1):
                mapping[word[:length]] += 1

        result = list()
        for word in words:
            score = 0
            for length in range(1, len(word)+1):
                score += mapping[word[:length]]

            result.append(score)

        return result
```

Method 2 (Trie Tree, Time Complexity: $O(N*K)$, Space Complexity: $O(N*K)$) :
```python
class Node:
    amount: int = 0
    children: dict = None

    def __init__(self):
        self.children = dict()

class Trie:
    nodes: dict[Node] = None

    def __init__(self):
        self.nodes = dict()

    def add(self, word: str):
        current: dict = self.nodes
        for char in word:
            if char not in current.keys():
                current[char] = Node()

            current[char].amount += 1
            current = current[char].children

    def get_score(self, word: str) -> int:
        score: int = 0
        current: dict = self.nodes
        for char in word:
            score += current[char].amount
            current = current[char].children

        return score

class Solution:
    def sumPrefixScores(self, words: List[str]) -> List[int]:
        trie = Trie()
        for word in words:
            trie.add(word)

        result = []
        for word in words:
            score = trie.get_score(word)
            result.append(score)

        return result
```

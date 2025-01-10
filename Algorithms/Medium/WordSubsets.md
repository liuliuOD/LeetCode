![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 916. [Word Subsets](https://leetcode.com/problems/word-subsets)

### Solution :

Method 1 (Brute Force, Time Complexity: $O(M+N)$, Space Complexity: $O(N)$ (M: the number of the elements in `words1`, N: the number of the elements in `words2`)) :
```rust
const BASE: u8 = b'a';

impl Solution {
    pub fn word_subsets(words1: Vec<String>, words2: Vec<String>) -> Vec<String> {
        let n: usize = words2.len();
        let mut counter_subset: Vec<[i32; 26]> = vec![[0; 26]; n];
        for (index, &ref word_subset) in words2.iter().enumerate() {
            for ascii in word_subset.bytes() {
                counter_subset[index][(ascii - BASE) as usize] += 1;
            }
        }
        let mut counter_maximum: [i32; 26] = [0; 26];
        for counter in counter_subset {
            for index in 0..26 {
                counter_maximum[index] = i32::max(counter_maximum[index], counter[index]);
            }
        }

        let mut result: Vec<String> = Vec::new();
        for word in words1 {
            let mut counter_target: [i32; 26] = [0; 26];
            for ascii in word.bytes() {
                counter_target[(ascii-BASE) as usize] += 1;
            }

            let mut valid: bool = true;
            for index in 0..26 {
                if counter_target[index] < counter_maximum[index] {
                    valid = false;
                    break;
                }
            }

            if valid {
                result.push(word);
            }
        }

        return result
    }
}
```

Method 2 (Time Complexity: $O(M+N)$, Space Complexity: $O(1)$ (M: the number of the elements in `words1`, N: the number of the elements in `words2`)) :
```rust
const BASE: u8 = b'a';

impl Solution {
    pub fn word_subsets(words1: Vec<String>, words2: Vec<String>) -> Vec<String> {
        let n: usize = words2.len();
        let mut counter_maximum: [i32; 26] = [0; 26];
        for word_subset in words2 {
            let mut counter_candidate: [i32; 26] = [0; 26];
            for ascii in word_subset.bytes() {
                counter_candidate[(ascii - BASE) as usize] += 1;
            }

            for index in 0..26 {
                counter_maximum[index] = i32::max(counter_maximum[index], counter_candidate[index]);
            }
        }

        let mut result: Vec<String> = Vec::new();
        for word in words1 {
            let mut counter_target: [i32; 26] = [0; 26];
            for ascii in word.bytes() {
                counter_target[(ascii-BASE) as usize] += 1;
            }

            let mut valid: bool = true;
            for index in 0..26 {
                if counter_target[index] < counter_maximum[index] {
                    valid = false;
                    break;
                }
            }

            if valid {
                result.push(word);
            }
        }

        return result
    }
}
```

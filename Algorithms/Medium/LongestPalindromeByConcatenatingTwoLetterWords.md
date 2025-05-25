![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 2131. [Longest Palindrome By Concatenating Two Letter Words](https://leetcode.com/problems/longest-palindrome-by-concatenating-two-letter-words)

### Solution :

Method 1 (AI by Grok3, Time Complexity: $O(N)$, Space Complexity: $O(N)$ (N: the number of elements in `words`)) :
```rust
use std::collections::HashMap;

impl Solution {
    pub fn longest_palindrome(words: Vec<String>) -> i32 {
        let mut freq: HashMap<String, i32> = HashMap::new();
        let mut has_odd = false;
        let mut total_pairs = 0;

        // Count frequency of each word
        for word in &words {
            *freq.entry(word.clone()).or_insert(0) += 1;
        }

        for word in &words {
            let rev: String = word.chars().rev().collect();
            if word == &rev {
                // Palindromic word
                let count = freq[word];
                let pairs = count / 2;
                total_pairs += pairs;
                if count % 2 == 1 {
                    has_odd = true;
                }
                // Remove used pairs to avoid double counting
                *freq.get_mut(word).unwrap() -= pairs * 2;
            } else if freq.contains_key(&rev) && freq[word] > 0 && freq[&rev] > 0 {
                // Non-palindromic pair
                let min_count = std::cmp::min(freq[word], freq[&rev]);
                total_pairs += min_count;
                *freq.get_mut(word).unwrap() -= min_count;
                *freq.get_mut(&rev).unwrap() -= min_count;
            }
        }

        // Calculate total length
        let mut length = total_pairs * 4; // Each pair contributes 4 characters
        if has_odd {
            length += 2; // Add middle palindromic word
        }

        return length
    }
}
```

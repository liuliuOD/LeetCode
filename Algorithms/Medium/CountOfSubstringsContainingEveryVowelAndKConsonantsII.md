![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 3306. [Count Of Substrings Containing Every Vowel And K Consonants II](https://leetcode.com/problems/count-of-substrings-containing-every-vowel-and-k-consonants-ii)

### Solution :

Method 1 (AI by Grok3, Sliding Window, Time Complexity: $O(N)$, Space Complexity: $O(N)$ (N: the number of elements in `word`)) :
```rust
use std::collections::HashMap;

impl Solution {
    pub fn count_of_substrings(word: String, k: i32) -> i64 {
        // Convert k to i32 and use inclusion-exclusion
        let k = k as i32;
        return Self::count_at_least(&word, k) - Self::count_at_least(&word, k + 1)
    }

    fn count_at_least(s: &str, k: i32) -> i64 {
        let mut ans = 0;
        let mut left = 0;
        let mut consonant_count = 0;
        let mut vowel_count: HashMap<char, i32> = HashMap::new();
        let chars: Vec<char> = s.chars().collect();
        let n = chars.len();

        for right in 0..n {
            // Process current character
            if Self::is_vowel(chars[right]) {
                *vowel_count.entry(chars[right]).or_insert(0) += 1;
            } else {
                consonant_count += 1;
            }

            // Shrink window until we no longer satisfy conditions
            while left <= right && consonant_count >= k && vowel_count.len() == 5 {
                ans += (n - right) as i64; // All substrings ending at right

                // Remove leftmost character
                if Self::is_vowel(chars[left]) {
                    let count = vowel_count.get_mut(&chars[left]).unwrap();
                    *count -= 1;
                    if *count == 0 {
                        vowel_count.remove(&chars[left]);
                    }
                } else {
                    consonant_count -= 1;
                }
                left += 1;
            }
        }

        return ans
    }

    fn is_vowel(c: char) -> bool {
        return matches!(c, 'a' | 'e' | 'i' | 'o' | 'u')
    }
}
```

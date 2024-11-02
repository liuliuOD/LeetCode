![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-JAVA](https://img.shields.io/badge/Java-ED8B00?style=for-the-badge&logo=openjdk)
---

## 2490. [Circular Sentence](https://leetcode.com/problems/circular-sentence)

### Solution :

Method 1 (Brute Force, Time Complexity: $O(N)$, Space Complexity: $O(N)$ (N: the length of `sentence`)) :
```Rust
impl Solution {
    pub fn is_circular_sentence(sentence: String) -> bool {
        let n: usize = sentence.len();
        let sentence_char: Vec<char> = sentence.chars().collect();
        let mut char_previous: char = '?';
        for index in 0..n {
            let char_current: char = sentence_char[index];
            if char_current == ' ' {
                if char_previous != sentence_char[index+1] {
                    return false
                }

                continue;
            }

            char_previous = char_current;
        }

        return sentence_char[0] == char_previous
    }
}
```

### Solution :

Method 1 (Brute Force, Time Complexity: $O(N)$, Space Complexity: $O(N)$ (N: the length of `sentence`)) :
```java
class Solution {
    public boolean isCircularSentence(String sentence) {
        int n = sentence.length();
        char[] sentence_char = sentence.toCharArray();
        char char_previous = '?';
        for (int index=0; index<n; index++) {
            char char_current = sentence_char[index];
            if (char_current == ' ') {
                if (char_previous != sentence_char[index+1]) {
                    return false;
                }

                continue;
            }

            char_previous = char_current;
        }

        return sentence_char[0] == char_previous;
    }
}
```

Method 2 (Brute Force, Time Complexity: $O(N)$, Space Complexity: $O(N)$ (N: the length of `sentence`)) :
```java
class Solution {
    public boolean isCircularSentence(String sentence) {
        String[] sentences = sentence.split(" ");
        for (int index=1; index<sentences.length; index++) {
            if (sentences[index-1].charAt(sentences[index-1].length()-1) != sentences[index].charAt(0)) {
                return false;
            }
        }

        return sentence.charAt(0) == sentence.charAt(sentence.length()-1);
    }
}
```

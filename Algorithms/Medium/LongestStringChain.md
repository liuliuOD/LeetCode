![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
![language-PHP](https://img.shields.io/badge/%20-PHP-acb1f9?style=for-the-badge&logo=PHP)
---

## 1048. [Longest String Chain](https://leetcode.com/problems/longest-string-chain)

### Solution :

Method 1 (DFS, ERROR: "Time Limit Exceeded", 78/84, Time Complexity: $O(?)$) :
```python
class Solution:
    def longestStrChain(self, words: List[str]) -> int:
        mapping = defaultdict(list)
        for word in words:
            mapping[len(word)].append(word)

        result = 0
        for word in words:
            amount_items = 1 + self.dfs(word, mapping)
            result = max(result, amount_items)

        return result

    def dfs(self, word, mapping):
        n = len(word)
        if n+1 not in mapping:
            return 0

        result = 0
        for word_next in mapping[n+1]:
            pointer_word = pointer_next = 0
            while pointer_word < n and pointer_next < n+1:
                if word[pointer_word] == word_next[pointer_next]:
                    pointer_word += 1
                pointer_next += 1

            if pointer_word < n:
                continue

            result = max(result, 1 + self.dfs(word_next, mapping))

        return result
```

Method 2 (DFS + Memoization, Time Complexity: $O(M^2*N)$ (where M = amount in list of `words`, N = maximum length of word in words)) :
```python
class Solution:
    def longestStrChain(self, words: List[str]) -> int:
        mapping = defaultdict(list)
        for word in words:
            mapping[len(word)].append(word)

        memoization = {}
        result = 0
        for word in words:
            amount_items = 1 + self.dfs(word, memoization, mapping)
            result = max(result, amount_items)

        return result

    def dfs(self, word, memoization, mapping):
        if word in memoization:
            return memoization[word]

        n = len(word)
        if n+1 not in mapping:
            return 0

        result = 0
        for word_next in mapping[n+1]:
            pointer_word = pointer_next = 0
            while pointer_word < n and pointer_next < n+1:
                if word[pointer_word] == word_next[pointer_next]:
                    pointer_word += 1
                pointer_next += 1

            if pointer_word < n:
                continue

            result = max(result, 1 + self.dfs(word_next, memoization, mapping))

        memoization[word] = result

        return result
```

Method 3 (Dynamic Programming, Time Complexity: $O(M^2*N)$) :
```python
class Solution:
    def longestStrChain(self, words: List[str]) -> int:
        mapping = defaultdict(list)
        for word in words:
            mapping[len(word)].append(word)

        words.sort(key=lambda item: len(item))
        dp = {word: 1 for word in words}
        for word in words:
            n = len(word)
            if n-1 not in mapping:
                continue

            for word_previous in mapping[n-1]:
                pointer_word = pointer_previous = 0
                while pointer_previous < n-1 and pointer_word < n:
                    if word_previous[pointer_previous] == word[pointer_word]:
                        pointer_previous += 1
                    pointer_word += 1

                if pointer_previous < n-1:
                    continue

                dp[word] = max(dp[word], 1+dp[word_previous])

        return max(dp.values())
```

Method 4 (DFS, Time Complexity: $O(M*N)$) :
```python
class Solution:
    def longestStrChain(self, words: List[str]) -> int:
        existed = set(words)
        memoization = {}
        result = 0
        for word in words:
            result = max(result, self.dfs(word, memoization, existed, words))

        return result

    def dfs(self, word, memoization, existed, words) -> int:
        if word not in existed:
            return 0

        if word in memoization:
            return memoization[word]

        result = 1
        for index_remove in range(len(word)):
            word_next = word[:index_remove] + word[index_remove+1:]
            result = max(result, 1 + self.dfs(word_next, memoization, existed, words))

        memoization[word] = result
        return result
```

Method 5 (Dynamic Programming, Time Complexity: $O(M*N)$) :
```python
class Solution:
    def longestStrChain(self, words: List[str]) -> int:
        words.sort(key=len)
        dp = {}
        for word in words:
            dp[word] = 1
            for index in range(len(word)):
                word_previous = word[:index] + word[index+1:]
                if word_previous not in dp:
                    continue

                dp[word] = max(dp[word], 1+dp[word_previous])

        return max(dp.values())
```

### Solution :

Method 1 (Dynamic Programming) :
```php
class Solution {

    /**
     * @param String[] $words
     * @return Integer
     */
    function longestStrChain($words) {
        usort($words, function ($a, $b) {
            return strlen($a) <=> strlen($b);
        });
        $dp = [];
        foreach($words as $word) {
            $dp[$word] = 1;
            for($indexRemove = 0; $indexRemove < strlen($word); $indexRemove++) {
                $wordPrevious = substr($word, 0, $indexRemove) . substr($word, $indexRemove+1);
                if (isset($dp[$wordPrevious])) {
                    $dp[$word] = max($dp[$word], 1 + $dp[$wordPrevious]);
                }
            }
        }

        return max($dp);
    }
}
```

Method 2 (DFS + Memoization) :
```php
class Solution {

    /**
     * @param String[] $words
     * @return Integer
     */
    function longestStrChain($words) {
        $memoization = [];
        $result = 0;
        $keyWords = array_flip($words);
        foreach($words as $word) {
            $result = max($result, $this->dfs($word, $memoization, $keyWords));
        }

        return $result;
    }

    function dfs($word, &$memoization, $keyWords) : Int {
        if (!isset($keyWords[$word])) {
            return 0;
        }

        if (isset($memoization[$word])) {
            return $memoization[$word];
        }

        $result = 1;
        for ($indexRemove = 0; $indexRemove < strlen($word); $indexRemove++) {
            $wordPrevious = substr($word, 0, $indexRemove) . substr($word, $indexRemove+1);
            $result = max($result, 1+$this->dfs($wordPrevious, $memoization, $keyWords));
        }

        return $memoization[$word] = $result;
    }
}
```

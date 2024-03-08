![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
![language-PHP](https://img.shields.io/badge/PHP-acb1f9?style=for-the-badge&logo=PHP)
---

## 392. [Is Subsequence](https://leetcode.com/problems/is-subsequence)

### Solution :

Method 1 (Adjust List + Brute Force) :
```python
class Solution:
    def isSubsequence(self, s: str, t: str) -> bool:
        mapping = defaultdict(list)
        for index_t, ch_t in enumerate(t):
            for ch_s in s:
                if ch_s == ch_t:
                    mapping[ch_s].append(index_t)

        temp = -1
        for ch_s in s:
            if ch_s not in mapping:
                return False

            heapq.heapify(mapping[ch_s])
            while mapping[ch_s]:
                index_s = heapq.heappop(mapping[ch_s])
                if index_s > temp:
                    temp = index_s
                    break

                if len(mapping[ch_s]) == 0:
                    return False
        return True
```

Method 2 (Two Pointer) :
```python
class Solution:
    def isSubsequence(self, s: str, t: str) -> bool:
        if len(s) == 0:
            return True

        pointer_s = 0
        for ch_t in t:
            if ch_t == s[pointer_s]:
                pointer_s += 1
            if pointer_s == len(s):
                return True
        return False
```

Method 3 (Two Pointer + add default string `=`) :
```python
class Solution:
    def isSubsequence(self, s: str, t: str) -> bool:
        s = '=' + s
        t = '=' + t
        pointer_s = 0
        for ch_t in t:
            if pointer_s < len(s) and ch_t == s[pointer_s]:
                pointer_s += 1
            if pointer_s == len(s):
                return True
        return False
```

Method 4 (Dynamic Programming) :
```python
class Solution:
    def isSubsequence(self, s: str, t: str) -> bool:
        len_s = len(s)
        len_t = len(t)
        # add '=' to position 0, to set init status when either `s` or `t` is empty string
        s = '=' + s
        t = '=' + t
        dp = [[1] + [0] * len_s for _ in range(len_t+1)]

        for index_t, index_s in product(range(1, len_t+1), range(1, len_s+1)):
            dp[index_t][index_s] = dp[index_t-1][index_s-1] if t[index_t] == s[index_s] else dp[index_t-1][index_s]

        return dp[-1][-1]
```

Method 5 (Hash Map) :
```python
class Solution:
    def isSubsequence(self, s: str, t: str) -> bool:
        m = len(s)
        n = len(t)
        if m > n:
            return False

        mapping = defaultdict(list)
        for index, char in enumerate(t):
            mapping[char].append(index)

        index_previous = -1
        for char in s:
            if char not in mapping:
                return False

            index_temp = float('inf')
            for index_next in mapping[char]:
                if index_next <= index_previous:
                    continue

                index_temp = min(index_temp, index_next)

            if index_temp == float('inf'):
                return False
            index_previous = index_temp

        return True
```

### Solution:

Method 1 (Two Pointer, Time Complexity: $O(M+N)$) :
```php
class Solution {

    /**
     * @param String $s
     * @param String $t
     * @return Boolean
     */
    function isSubsequence($s, $t) {
        $m = strlen($s);
        $n = strlen($t);
        if ($m > $n) {
            return false;
        }

        $pointerS = $pointerT = 0;
        while ($pointerS < $m) {
            if ($pointerT >= $n) {
                return false;
            }

            # Option 1
            if ($s[$pointerS] == $t[$pointerT]) {
                $pointerS++;
                $pointerT++;
            } else {
                $pointerT++;
            }
            /**
             * # Option 2
             *
             * if ($s[$pointerS] == $t[$pointerT]) {
             *     $pointerS++;
             * }
             *
             * $pointerT++;
             */
        }

        return true;
    }
}
```

Method 2 (Dynamic Programming, Time Complexity: $O(N^2)$) :
```php
class Solution {

    /**
     * @param String $s
     * @param String $t
     * @return Boolean
     */
    function isSubsequence($s, $t) {
        $m = strlen($s);
        $n = strlen($t);
        $dp = array_fill(0, $m+1, []);
        
        /**
         * dp[m][n] means how many characters that the first `m` characters in $s, included in the first `n` characters in $t.
         */
        for ($indexM = 1; $indexM <= $m; $indexM++) {
            for ($indexN = 1; $indexN <= $n; $indexN++) {
                $dp[$indexM][$indexN] = $s[$indexM-1] == $t[$indexN-1]
                    ? 1 + $dp[$indexM-1][$indexN-1]
                    : max($dp[$indexM-1][$indexN], $dp[$indexM][$indexN-1]);
            }
        }

        return $dp[$m][$n] == $m;
    }
}
```

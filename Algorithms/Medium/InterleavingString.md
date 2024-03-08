![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
![language-PHP](https://img.shields.io/badge/PHP-acb1f9?style=for-the-badge&logo=PHP)
---

## 97. [Interleaving String](https://leetcode.com/problems/interleaving-string)

### Solution :

Method 1 (DFS, ERROR: "Time Limit Exceeded", 93/106) :
```python
class Solution:
    def isInterleave(self, s1: str, s2: str, s3: str) -> bool:
        return self.dfs(s1, s2, s3)

    def dfs(self, s1: str, s2: str, s3: str) -> bool:
        if s3 == '':
            return True

        if len(s1) + len(s2) != len(s3):
            return False

        result = False
        if s1 and s1[0] == s3[0]:
            result |= self.dfs(s1[1:], s2, s3[1:])
        if s2 and s2[0] == s3[0]:
            result |= self.dfs(s1, s2[1:], s3[1:])

        return result
```

Method 2 (DFS + Memoization) :
```python
class Solution:
    def isInterleave(self, s1: str, s2: str, s3: str) -> bool:
        if len(s1) + len(s2) != len(s3):
            return False

        memoization: Dict[Tuple[str, str], bool] = {}
        return self.dfs(s1, s2, s3, memoization)

    def dfs(self, s1: str, s2: str, s3: str, memoization: Dict[Tuple[str, str], bool]) -> bool:
        if s3 == '':
            return True

        result = False
        if s1 and s1[0] == s3[0]:
            key = (s1[1:], s2)
            if key not in memoization:
                memoization[key] = self.dfs(key[0], key[1], s3[1:], memoization)
            result |= memoization[key]
        if s2 and s2[0] == s3[0]:
            key = (s1, s2[1:])
            if key not in memoization:
                memoization[key] = self.dfs(key[0], key[1], s3[1:], memoization)
            result |= memoization[key]

        memoization[(s1, s2)] = result

        return result
```

Method 3 (DFS + Memoization) :
```python
class Solution:
    def isInterleave(self, s1: str, s2: str, s3: str) -> bool:
        if len(s1) + len(s2) != len(s3):
            return False

        memoization: Dict[Tuple[str, str], bool] = {}
        return self.dfs(s1, s2, s3, memoization)

    def dfs(self, s1: str, s2: str, s3: str, memoization: Dict[Tuple[str, str], bool]) -> bool:
        if s3 == '':
            return True

        key_current = (s1, s2)
        if key_current in memoization:
            return memoization[key_current]

        result = False
        if s1 and s1[0] == s3[0]:
            key = (s1[1:], s2)
            result |= self.dfs(key[0], key[1], s3[1:], memoization)
        if s2 and s2[0] == s3[0]:
            key = (s1, s2[1:])
            result |= self.dfs(key[0], key[1], s3[1:], memoization)

        memoization[key_current] = result

        return result
```

Method 4 (Dynamic Programming, 2D) :
```python
class Solution:
    def isInterleave(self, s1: str, s2: str, s3: str) -> bool:
        len_1, len_2, len_3 = len(s1), len(s2), len(s3)
        if len_1+len_2 != len_3:
            return False

        # dp[contribution amount of s1][contribution amount of s2]
        dp = [[False]*(len_2+1) for _ in range(len_1+1)]
        dp[0][0] = True
        for index in range(0, len_1):
            index_dp = index + 1
            dp[index_dp][0] = dp[index_dp-1][0] and s1[index] == s3[index]
        for index in range(0, len_2):
            index_dp = index + 1
            dp[0][index_dp] = dp[0][index_dp-1] and s2[index] == s3[index]

        for index_1 in range(len_1):
            index_dp_1 = index_1 + 1
            for index_2 in range(len_2):
                index_dp_2 = index_2 + 1
                dp[index_dp_1][index_dp_2] = (dp[index_dp_1-1][index_dp_2] and s1[index_1] == s3[index_1+index_2+1]) or (dp[index_dp_1][index_dp_2-1] and s2[index_2] == s3[index_1+index_2+1])
        return dp[len_1][len_2]
```

Method 5 (Dynamic Programming, 1D) :
```python
class Solution:
    def isInterleave(self, s1: str, s2: str, s3: str) -> bool:
        len_1, len_2, len_3 = len(s1), len(s2), len(s3)
        if len_1+len_2 != len_3:
            return False

        dp = [False] * (len_2 + 1)
        dp[0] = True
        for index in range(len_2):
            dp[index+1] = dp[index] and s2[index] == s3[index]

        for index_1 in range(len_1):
            dp[0] &= s1[index_1] == s3[index_1]
            index_dp_1 = index_1 + 1
            for index_2 in range(len_2):
                index_dp_2 = index_2 + 1
                dp[index_dp_2] = (dp[index_dp_2] and s1[index_1] == s3[index_1+index_2+1]) or (dp[index_dp_2-1] and s2[index_2] == s3[index_1+index_2+1])
        return dp[len_2]
```

### Solution :

Method 1 (DFS + Memoization) :
```php
class Solution {

    /**
     * @param String $s1
     * @param String $s2
     * @param String $s3
     * @return Boolean
     */
    function isInterleave($s1, $s2, $s3) {
        if (strlen($s1)+strlen($s2) !== strlen($s3)) {
            return false;
        }

        $memoization = [];
        return $this->dfs($s1, $s2, $s3, $memoization);
    }

    function dfs(String $s1, String $s2, String $s3, Array &$memoization) {
        if ($s3 === '') {
            return true;
        }

        $key = sprintf('%s-%s', $s1, $s2);
        if (isset($memoization[$key])) {
            return $memoization[$key];
        }

        $result = false;
        $subS3 = substr($s3, 1, strlen($s3)-1);
        if ($s1 && $s1[0] == $s3[0]) {
            $result |= $this->dfs(substr($s1, 1, strlen($s1)-1), $s2, $subS3, $memoization);
        }
        if ($s2 && $s2[0] == $s3[0]) {
            $result |= $this->dfs($s1, substr($s2, 1, strlen($s2)-1), $subS3, $memoization);
        }

        return $memoization[$key] = $result;
    }
}
```

Method 2 (Dynamic Programming, 1D) :
```php
class Solution {

    /**
     * @param String $s1
     * @param String $s2
     * @param String $s3
     * @return Boolean
     */
    function isInterleave($s1, $s2, $s3) {
        if (strlen($s1)+strlen($s2) !== strlen($s3)) {
            return false;
        }

        $amount2 = strlen($s2);
        $dp = array_fill(0, $amount2, false);
        $dp[0] = true;

        foreach(str_split($s2) as $index => $char) {
            $dp[$index+1] = $dp[$index] && $char == $s3[$index];
        }

        foreach(str_split($s1) as $indexS1 => $char1) {
            $dp[0] &= $char1 == $s3[$indexS1];
            foreach(str_split($s2) as $indexS2 => $char2) {
                $indexS3 = $indexS1 + $indexS2 + 1;
                $dp[$indexS2+1] = ($dp[$indexS2+1] && $s1[$indexS1] == $s3[$indexS3]) || ($dp[$indexS2] && $s2[$indexS2] == $s3[$indexS3]);
            }
        }

        return $dp[$amount2];
    }
}
```

![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2800. [Shortest String That Contains Three Strings](https://leetcode.com/problems/shortest-string-that-contains-three-strings)

### Solution :

Method 1 (Brute Force) :
```python
class Solution:
    def minimumString(self, a: str, b: str, c: str) -> str:
        result: List[str] = []
        self.dfs('', [a, b, c], result)

        minimum = float('inf')
        for string in result:
            minimum = min(minimum, len(string))

        return min(list(filter(lambda string: len(string) == minimum, result)))

    def dfs(self, string: str, strings: List[str], result: List[str]):
        if len(strings) == 0:
            result.append(string)
            return None

        for index in range(len(strings)):
            # we need to rotate string order to deal with case like ['cab', 'a', 'b']
            self.dfs(self.concatString(string, strings[index]), strings[:index]+strings[index+1:], result)
            self.dfs(self.concatString(strings[index], string), strings[:index]+strings[index+1:], result)

    def concatString(self, left: str, right: str) -> str:
        pointer_left = pointer_right = 0
        while pointer_left <= pointer_right:
            index_right = 0
            while pointer_right < len(left) and index_right < len(right) and left[pointer_right] == right[index_right]:
                index_right += 1
                pointer_right += 1

            if pointer_right == len(left):
                return left + right[index_right:]

            if index_right == len(right):
                return left

            pointer_left += 1
            pointer_right = pointer_left

        return left + right
```

Method 2 (Brute Force + Bitmask) :
```python
class Solution:
    def minimumString(self, a: str, b: str, c: str) -> str:
        result: List[str] = []
        strings = [a, b, c]
        self.dfs('', 0, result, strings)

        minimum = float('inf')
        for string in result:
            minimum = min(minimum, len(string))

        return min(list(filter(lambda string: len(string) == minimum, result)))

    def dfs(self, string: str, bitmask: int, result: List[str], strings: List[str]):
        if bitmask == (1<<len(strings))-1:
            result.append(string)
            return None

        for index in range(len(strings)):
            if bitmask & 1<<index:
                continue

            bitmask_next = bitmask | 1<<index
            self.dfs(self.concatString(string, strings[index]), bitmask_next, result, strings)
            self.dfs(self.concatString(strings[index], string), bitmask_next, result, strings)

    def concatString(self, left: str, right: str) -> str:
        pointer_left = pointer_right = 0
        while pointer_left <= pointer_right:
            index_right = 0
            while pointer_right < len(left) and index_right < len(right) and left[pointer_right] == right[index_right]:
                index_right += 1
                pointer_right += 1

            if pointer_right == len(left):
                return left + right[index_right:]

            if index_right == len(right):
                return left

            pointer_left += 1
            pointer_right = pointer_left

        return left + right
```

Method 3 (Brute Force + Bitmask) :
```python
class Solution:
    def minimumString(self, a: str, b: str, c: str) -> str:
        result: List[str] = []
        strings = [a, b, c]
        self.dfs('', 0, result, strings)

        minimum = float('inf')
        for string in result:
            minimum = min(minimum, len(string))

        return min(list(filter(lambda string: len(string) == minimum, result)))

    def dfs(self, string: str, bitmask: int, result: List[str], strings: List[str]):
        if bitmask == (1<<len(strings))-1:
            result.append(string)
            return None

        for index in range(len(strings)):
            if bitmask & 1<<index:
                continue

            bitmask_next = bitmask | 1<<index
            self.dfs(self.concatString(string, strings[index]), bitmask_next, result, strings)

    def concatString(self, left: str, right: str) -> str:
        # to process case like ['cab', 'a', 'b']
        if left in right:
            return right
        if right in left:
            return left

        pointer_left = pointer_right = 0
        while pointer_left <= pointer_right:
            index_right = 0
            while pointer_right < len(left) and index_right < len(right) and left[pointer_right] == right[index_right]:
                index_right += 1
                pointer_right += 1

            if pointer_right == len(left):
                return left + right[index_right:]

            if index_right == len(right):
                return left

            pointer_left += 1
            pointer_right = pointer_left

        return left + right
```

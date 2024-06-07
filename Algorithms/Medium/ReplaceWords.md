![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 648. [Replace Words](https://leetcode.com/problems/replace-words)

### Solution :

Method 1 (Brute Force, Time Complexity: $O(M*N*Q)$ (M: average length of the words in `sentence` and `dictionary`, N: amount of the words in `sentence`, Q: amount of the words in `dictionary`), Space Complexity: $O(M*N)$) :
```python
class Solution:
    def replaceWords(self, dictionary: List[str], sentence: str) -> str:
        result = sentence.split(" ")
        dictionary.sort()
        for index in range(len(result)):
            for root in dictionary:
                if result[index].startswith(root):
                    result[index] = root
                    break

        return " ".join(result)
```

Method 2 (Hash Set, Time Complexity: $O(M*(N+Q))$ (M: average length of the words in `sentence` and `dictionary`, N: amount of the words in `sentence`, Q: amount of the words in `dictionary`), Space Complexity: $O(M*(N+Q))$) :
```python
class Solution:
    def replaceWords(self, dictionary: List[str], sentence: str) -> str:
        result = sentence.split(" ")
        dictionary_set = set(dictionary)
        for index in range(len(result)):
            derive = result[index]
            for index_derive in range(len(derive)):
                if derive[:index_derive+1] in dictionary_set:
                    result[index] = derive[:index_derive+1]
                    break

        return " ".join(result)
```

Method 3 (Trie Tree + Hash Map, Time Complexity: $O(M*(N+Q))$ (M: average length of the words in `sentence` and `dictionary`, N: amount of the words in `sentence`, Q: amount of the words in `dictionary`), Space Complexity: $O(M*(N+Q))$) :
```python
class TrieNode:
    def __init__(self):
        self.is_ended = False
        self.nodes: dict[str, TrieNode] = {}

class TrieTree:
    def __init__(self):
        self.root = TrieNode()

    def append(self, word: str):
        node = self.root
        for char in word:
            if char not in node.nodes.keys():
                node.nodes[char] = TrieNode()

            node = node.nodes[char]

        node.is_ended = True

    def find(self, word: str) -> str:
        node = self.root

        for index, char in enumerate(word):
            if node.is_ended:
                return word[:index]

            if char not in node.nodes:
                break

            node = node.nodes[char]

        return word

class Solution:
    def replaceWords(self, dictionary: List[str], sentence: str) -> str:
        trie_tree = TrieTree()
        for word in dictionary:
            trie_tree.append(word)

        result: list[str] = []
        for word in sentence.split(" "):
            result.append(trie_tree.find(word))

        return " ".join(result)
```

Method 4 (Trie Tree + Array, Time Complexity: $O(M*(N+Q))$ (M: average length of the words in `sentence` and `dictionary`, N: amount of the words in `sentence`, Q: amount of the words in `dictionary`), Space Complexity: $O(M*(N+Q))$) :
```python
BASE = ord("a")

class TrieNode:
    def __init__(self):
        self.is_ended = False
        self.nodes: list[TrieNode] = [None] * 26

class TrieTree:
    def __init__(self):
        self.root = TrieNode()

    def append(self, word: str):
        node = self.root
        for char in word:
            ascii_char = ord(char) - BASE
            if node.nodes[ascii_char] is None:
                node.nodes[ascii_char] = TrieNode()

            node = node.nodes[ascii_char]

        node.is_ended = True

    def find(self, word: str) -> str:
        node = self.root

        for index in range(len(word)):
            ascii_char = ord(word[index]) - BASE
            if node.is_ended:
                return word[:index]

            if node.nodes[ascii_char] is None:
                break

            node = node.nodes[ascii_char]

        return word

class Solution:
    def replaceWords(self, dictionary: List[str], sentence: str) -> str:
        trie_tree = TrieTree()
        for word in dictionary:
            trie_tree.append(word)

        result: list[str] = []
        for word in sentence.split(" "):
            result.append(trie_tree.find(word))

        return " ".join(result)
```

![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 380. [Insert Delete GetRandom O(1)](https://leetcode.com/problems/insert-delete-getrandom-o1)

### Solution :

```python
# Your RandomizedSet object will be instantiated and called as such:
# obj = RandomizedSet()
# param_1 = obj.insert(val)
# param_2 = obj.remove(val)
# param_3 = obj.getRandom()
```

Method 1 (Set) :
```python
class RandomizedSet:

    def __init__(self):
        self.items = set()

    def insert(self, val: int) -> bool:
        if val in self.items:
            return False

        self.items.add(val)
        return True

    def remove(self, val: int) -> bool:
        if val not in self.items:
            return False

        self.items.remove(val)
        return True

    def getRandom(self) -> int:
        return random.choice(list(self.items))
```

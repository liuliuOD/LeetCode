![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 341. [Flatten Nested List Iterator](https://leetcode.com/problems/flatten-nested-list-iterator)

### Solution :

```python
# """
# This is the interface that allows for creating nested lists.
# You should not implement it, or speculate about its implementation
# """
#class NestedInteger:
#    def isInteger(self) -> bool:
#        """
#        @return True if this NestedInteger holds a single integer, rather than a nested list.
#        """
#
#    def getInteger(self) -> int:
#        """
#        @return the single integer that this NestedInteger holds, if it holds a single integer
#        Return None if this NestedInteger holds a nested list
#        """
#
#    def getList(self) -> [NestedInteger]:
#        """
#        @return the nested list that this NestedInteger holds, if it holds a nested list
#        Return None if this NestedInteger holds a single integer
#        """
```

Method 1 (Recursive) :
```python
class NestedIterator:
    def __init__(self, nested_list: [NestedInteger]):
        self.index = 0
        self.items = []
        self.__flatten(nested_list)

    def __flatten(self, item_nested):
        for item in item_nested:
            if item.isInteger():
                self.items.append(item.getInteger())
                continue

            self.__flatten(item.getList())

    def next(self) -> int:
        temp = self.items[self.index]
        self.index += 1

        return temp

    def hasNext(self) -> bool:
         return self.index < len(self.items)
```

Method 2 (Stack) :
```python
class NestedIterator:
    def __init__(self, nested_list: [NestedInteger]):
        self.items = nested_list[::-1]

    def next(self) -> int:
        return self.items.pop().getInteger()

    def hasNext(self) -> bool:
        while self.items:
            top = self.items[-1]
            if top.isInteger():
                return True

            self.items.pop()
            self.items += top.getList()[::-1]

        return False
```

```python
# Your NestedIterator object will be instantiated and called as such:
# i, v = NestedIterator(nestedList), []
# while i.hasNext(): v.append(i.next())
```

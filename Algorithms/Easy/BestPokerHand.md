![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2347. [Best Poker Hand](https://leetcode.com/problems/best-poker-hand)

### Solution :

Method 1 (Brute Force, Time Complexity: $O(N)$) :
```python
class Solution:
    def bestHand(self, ranks: List[int], suits: List[str]) -> str:
        mapping_suits = Counter(suits)
        mapping_ranks = Counter(ranks)

        results = set()
        for group in mapping_suits.values():
            if group == 5:
                return 'Flush'
            else:
                results.add('High Card')
        for group in mapping_ranks.values():
            if group >= 3:
                return 'Three of a Kind'
            if group == 2:
                results.add('Pair')

        return 'Pair' if 'Pair' in results else 'High Card'
```

Method 2 (Brute Force + Enumerate, Time Complexity: $O(N)$) :
```python
class HAND:
    five = 'Flush'
    three = 'Three of a Kind'
    two = 'Pair'
    one = 'High Card'

class Solution:
    def bestHand(self, ranks: List[int], suits: List[str]) -> str:
        mapping_suits = Counter(suits)
        mapping_ranks = Counter(ranks)

        results = set()
        for group in mapping_suits.values():
            if group == 5:
                return HAND.five
            else:
                results.add(HAND.one)
        for group in mapping_ranks.values():
            if group >= 3:
                return HAND.three
            if group == 2:
                results.add(HAND.two)

        return HAND.two if HAND.two in results else HAND.one
```

Method 3 (Counter + If) :
```python
class HAND:
    five = 'Flush'
    three = 'Three of a Kind'
    two = 'Pair'
    one = 'High Card'

class Solution:
    def bestHand(self, ranks: List[int], suits: List[str]) -> str:
        mapping_suits = Counter(suits)
        mapping_ranks = Counter(ranks)

        max_suits = max(mapping_suits.values())
        max_ranks = max(mapping_ranks.values())
        if max_suits == 5:
            return HAND.five
        if max_ranks >= 3:
            return HAND.three
        if max_ranks == 2:
            return HAND.two

        return HAND.one
```

Method 4 (Switch Case) :
```python
class HAND:
    five = 'Flush'
    three = 'Three of a Kind'
    two = 'Pair'
    one = 'High Card'

class Solution:
    def bestHand(self, ranks: List[int], suits: List[str]) -> str:
        if len(set(suits)) == 1:
            return HAND.five

        mapping_ranks = Counter(ranks)
        max_ranks = max(mapping_ranks.values())
        # Only for Python Version >= 3.10
        match max_ranks:
            case 3 | 4:
                return HAND.three
            case 2:
                return HAND.two
            case _:
                return HAND.one
```

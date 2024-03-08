![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 779. [K-th Symbol In Grammar](https://leetcode.com/problems/k-th-symbol-in-grammar)

### Inference :

```plainText
0 # n=1
0, 1 # n=2
0, 1, 1, 0 # n=3
0, 1, 1, 0, 1, 0, 0, 1 # n=4
0, 1, 1, 0, 1, 0, 0, 1, 1, 0, 0, 1, 0, 1, 1, 0 # n=5
```

### Solution :

Method 1 (ERROR: "Memory Limit Exceeded") :
```python
class Solution:
    def kthGrammar(self, n: int, k: int) -> int:
        base = [0]
        for power in range(1, n):
            temp = base
            for index in range(len(base)):
                temp.append((base[index]+1)%2)

            base = temp

        return base[k-1]
```

Method 2 (Recursive) :
```python
class Solution:
    def kthGrammar(self, n: int, k: int) -> int:
        if n == 1:
            return 0

        # calculate the length of grammar when n = n - 1
        amount_n_minus_1 = 2 ** (n-2)
        # bit will keep origin when the position `k` in the range of previous grammar's length
        if k <= amount_n_minus_1:
            return self.kthGrammar(n-1, k)

        # bit will be reversed when the position `k` over the range of previous grammar's length
        # Option 1
        return 1 - self.kthGrammar(n-1, k-amount_n_minus_1)
        """
        # Option 2

        return (1 + self.kthGrammar(n-1, k-amount_n_minus_1)) % 2
        """
```

Method 3 ([Reference](https://leetcode.com/problems/k-th-symbol-in-grammar/solutions/4205266/100-recursive-bit-count)) :
```python
class Solution:
    def kthGrammar(self, n: int, k: int) -> int:
        # convert the index of `k` to binary, count the number of 1s, and then take the remainder after dividing by 2
        return bin(k-1).count('1') % 2
```

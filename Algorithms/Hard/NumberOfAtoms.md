![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 726. [Number Of Atoms](https://leetcode.com/problems/number-of-atoms)

### Solution :

Method 1 (Brute Force + Stack) :
```python
class Solution:
    def countOfAtoms(self, formula: str) -> str:
        n = len(formula)
        parentheses: dict[int, int] = dict()
        stack = []
        index = 0
        while index < n:
            char = formula[index]
            if char == ")":
                index += 1
                amount = 0
                while index < n and formula[index].isdigit():
                    amount = amount*10 + int(formula[index])
                    index += 1

                multiplier = max(1, amount)
                parentheses[stack.pop()] = multiplier
                continue
            elif char == "(":
                stack.append(index)

            index += 1

        mapping = defaultdict(int)
        self.calculator(0, 1, mapping, formula, parentheses)

        return "".join(atom + ("" if mapping[atom] == 1 else str(mapping[atom])) for atom in sorted(mapping.keys()))

    def calculator(self, index: int, multiplier: int, mapping: dict[str, int], formula: str, parentheses: dict[int, int]) -> int:
        n = len(formula)
        if index >= n:
            return index

        atom = ""
        index_current = index
        while index_current < n:
            char = formula[index_current]
            if char.isalpha():
                # upper + upper
                if char.isupper() and atom:
                    mapping[atom] += multiplier
                    atom = ""

                atom += char
                index_current += 1
            elif char.isdigit():
                if not atom:
                    index_current += 1
                    continue

                amount = 0
                while index_current < n and formula[index_current].isdigit():
                    char = formula[index_current]
                    amount = amount*10 + int(char)
                    index_current += 1

                mapping[atom] += max(1, amount) * multiplier
                atom = ""
            elif char == "(":
                if atom:
                    mapping[atom] += multiplier
                    atom = ""

                index_current = self.calculator(index_current+1, multiplier*parentheses[index_current], mapping, formula, parentheses)
            elif char == ")":
                if atom:
                    mapping[atom] += multiplier

                return index_current + 1

        if atom:
            mapping[atom] += multiplier
```

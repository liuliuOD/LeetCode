![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 273. [Integer To English Words](https://leetcode.com/problems/integer-to-english-words)

### Solution :

Method 1 (Recursive) :
```python
BELOW_TWENTY = ["Zero", "One", "Two", "Three", "Four", "Five", "Six", "Seven", "Eight", "Nine", "Ten", "Eleven", "Twelve", "Thirteen", "Fourteen", "Fifteen", "Sixteen", "Seventeen", "Eighteen", "Nineteen"]
TIMES_OF_TEN = [None, "Ten", "Twenty", "Thirty", "Forty", "Fifty", "Sixty", "Seventy", "Eighty", "Ninety"]

class Solution:
    def numberToWords(self, num: int) -> str:
        if num <= 0:
            return BELOW_TWENTY[0]

        if num < 20:
            return BELOW_TWENTY[num]

        if num < 100:
            return "{}{}".format(TIMES_OF_TEN[num//10], f" {BELOW_TWENTY[num%10]}" if num%10 else "")

        if num < 1_000:
            return "{} Hundred{}".format(BELOW_TWENTY[num//100], f" {self.numberToWords(num%100)}" if num%100 else "")

        if num < 1_000_000:
            return "{} Thousand{}".format(self.numberToWords(num//1_000), f" {self.numberToWords(num%1_000)}" if num%1000 else "")

        if num < 1_000_000_000:
            return "{} Million{}".format(self.numberToWords(num//1_000_000), f" {self.numberToWords(num%1_000_000)}" if num%1_000_000 else "")

        if num < 1_000_000_000_000:
            return "{} Billion{}".format(self.numberToWords(num//1_000_000_000), f" {self.numberToWords(num%1_000_000_000)}" if num%1_000_000_000 else "")
```

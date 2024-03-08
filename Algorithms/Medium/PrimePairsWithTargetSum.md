![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2761. [Prime Pairs With Target Sum](https://leetcode.com/problems/prime-pairs-with-target-sum)

### Solution :

Method 1 (ERROR: "Time Limit Exceeded") :
```python
import math
class Solution:
    def findPrimePairs(self, n: int) -> List[List[int]]:
        primes = set()
        for value in range(2, n):
            if not self.isPrime(value):
                continue
            primes.add(value)

        result = set()
        for prime in primes:
            prime_2 = n-prime
            if prime_2 in primes:
                result.add((prime, prime_2) if prime < prime_2 else (prime_2, prime))
        return sorted(list(result), key=lambda x: x[0])

    def isPrime(self, n: int) -> bool:
        for i in range(2,int(math.sqrt(n))+1):
            if n%i == 0:
                return False
        return True
```

Method 2 ([Sieve of Eratosthenes](https://www.topcoder.com/thrive/articles/sieve-of-eratosthenes-algorithm)) :
```python
class Solution:
    def findPrimePairs(self, n: int) -> List[List[int]]:
        primes = self.getPrimes(n)
        result = []

        for index_prime in range(2, len(primes)):
            if primes[index_prime] == False:
                continue
            prime = index_prime
            pair = n - prime
            if pair < prime:
                continue
            
            if primes[pair] == False:
                continue
            
            result.append([prime, pair])

        return result

    def getPrimes(self, n: int) -> List[int]:
        primes = [True] * (n+1)
        primes[0], primes[1] = False, False

        current = 2
        while current**2 <= n:
            if primes[current] == False:
                current += 1
                continue
            for index in range(current**2, n+1, current):
                primes[index] = False

            current += 1

        return primes
```

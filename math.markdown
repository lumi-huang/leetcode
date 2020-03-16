### 204. Count Primes
```python
class Solution:
    def countPrimes(self, n: int) -> int:
        if n <= 2: return 0
        
        count = 1
        prime = [True]*n
        for i in range(3, n, 2):
            if prime[i]:
                count += 1
                j = 3
                while i*j < n:
                    prime[i*j] = False
                    j += 2
        return count
            
```

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

### 
```python
class Solution:
    def convertToBase7(self, num: int) -> str:
        p = 0
        output = ""
        if num == 0: return "0"
        if num < 0:
            output += "-"
            num = num * (-1)
        while 7**p <= num:
            p += 1
        p -= 1
        while p >= 0:
            output += str((num // (7**p)))
            num = num % 7**p
            p -= 1
        return output
```

## **Other Python Practices**  

### 125. Valid Palindrome
```python
class Solution:
    def isPalindrome(self, s: str) -> bool:
        s=re.sub('[^a-z\d]','',s.lower())
        return s==s[::-1]
```

### 242. Valid Anagram
```python
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        return sorted(s)==sorted(t)
```

```python
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        return all(s.count(i) == t.count(i) for i in 'abcdefghijklmnopqrstuvwxyz')
```

### 766. Toeplitz Matrix
```python
class Solution:
    def isToeplitzMatrix(self, matrix: List[List[int]]) -> bool:
        return all(r==0 or c==0 or matrix[r][c]==matrix[r-1][c-1]
                    for r, row in enumerate(matrix)
                   for c, val in enumerate(row))
```
```python
class Solution:
    def isToeplitzMatrix(self, matrix: List[List[int]]) -> bool:
        for r in range(1, len(matrix)):
            for c in range(1, len(matrix[0])):
                    if matrix[r][c] != matrix[r-1][c-1]: return False
        
        return True
```
```
class Solution:
    def isToeplitzMatrix(self, matrix: List[List[int]]) -> bool:
        return not any(matrix[r][c] != matrix[r-1][c-1] for r in range(1, len(matrix)) for c in range(1, len(matrix[0])))
```

### 941. Valid Mountain Array
```python
class Solution:
    def validMountainArray(self, arr: List[int]) -> bool:
        if len(arr)<3:
            return False
        up=down=0
        for i in range(len(arr)-1):
            if arr[i]<arr[i+1] and down==0:
                up+=1
            elif arr[i]>arr[i+1] and up>0:
                down+=1
            else:
                return False
        return up>0 and down >0 and (up+down == len(arr)-1)
```

### 1037. Valid Boomerang
```python
class Solution:
    def isBoomerang(self, points: List[List[int]]) -> bool:
        (x1, y1), (x2, y2), (x3, y3) = points
        return (x2-x1)*(y3-y2)-(x3-x2)*(y2-y1)!=0
```

### 1207. Unique Number of Occurrences
``` python
class Solution:
    def uniqueOccurrences(self, arr: List[int]) -> bool:
        hmap={}
        for i in arr:
            try:
                hmap[i] += 1
            except:
                hmap[i] = 1
        return len(hmap) == len(set(hmap.values()))
```

### 1550. Three Consecutive Odds
```python
class Solution:
    def threeConsecutiveOdds(self, arr: List[int]) -> bool:
        count=0
        for num in arr:
            if mod(num, 2)==1:
                count+=1
                if count==3: return True
            else: count=0
        return False
```
```python
class Solution:
    def threeConsecutiveOdds(self, arr: List[int]) -> bool:
        return any(len(t)==3 and t[0]%2==1 and t[1]%2==1 and t[2]%2==1 for t in zip(arr, arr[1:], arr[2:]))
```


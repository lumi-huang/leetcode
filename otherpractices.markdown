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

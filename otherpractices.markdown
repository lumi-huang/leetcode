## **Other Python Practices**  

### 2. Add Two Numbers
```python
class Solution:
    def addTwoNumbers(self, l1: ListNode, l2: ListNode) -> ListNode:
        out = cur = ListNode()
        s = 0
        while l1 or l2 or s>0:
            if l1:
                s+=l1.val
                l1=l1.next
            if l2:
                s+=l2.val
                l2=l2.next
            cur.next=ListNode(s%10)
            cur=cur.next
            s=s//10
        return out.next
```

### 3. Longest Substring Without Repeating Characters
```python
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        out = 0
        temp = ""
        for char in s:
            if char in temp:
                out = max(out, len(temp))
                temp=temp[temp.index(char)+1:]+char
            else:
                temp += char
        out = max(out,len(temp))
        return out
```

### 5. Longest Palindromic Substring
```python
class Solution:
    def longestPalindrome(self, s: str) -> str:
        head=0
        maximum=1
        
        for i in range(1,len(s)):
            low=i-1
            high=i
            while low>=0 and high<len(s) and s[low]==s[high]:
                if high-low+1>maximum:
                    head=low
                    maximum=high-low+1
                low-=1
                high+=1
                
            low=i-1
            high=i+1
            while low>=0 and high<len(s) and s[low]==s[high]:
                if high-low+1>maximum:
                    head=low
                    maximum=high-low+1
                low-=1
                high+=1
        
        return s[head:head+maximum]
    
   ```

### 21. Merge Two Sorted Lists
```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def mergeTwoLists(self, l1: ListNode, l2: ListNode) -> ListNode:
        out = cur = ListNode()
        if l1 == None:
            return l2
        if l2 == None:
            return l1
        while l1 and l2:
            if l1.val <= l2.val:
                cur.next = l1
                cur = cur.next
                l1 = l1.next
            else:
                cur.next = l2
                cur = cur.next
                l2 = l2.next
        if l1 == None:
            cur.next=l2
        if l2 == None:
            cur.next=l1
        return out.next
```
```python
class Solution:
    def mergeTwoLists(self, l1: ListNode, l2: ListNode) -> ListNode:
        if l1==None:
            return l2
        elif l2==None:
            return l1
        
        if l1.val <= l2.val:
            return ListNode(l1.val, self.mergeTwoLists(l1.next, l2))
        else:
            return ListNode(l2.val, self.mergeTwoLists(l1, l2.next))
```

### 27. Remove Element
```python
class Solution:
    def removeElement(self, nums: List[int], val: int) -> int:
        i=0
        j=0
        while j<len(nums):
            if nums[j]!=val:
                nums[i]=nums[j]
                i+=1
            j+=1
        return i
                
```
```python
class Solution:
    def removeElement(self, nums: List[int], val: int) -> int:
        while val in nums:
            nums.remove(val)
        return len(nums)
```

### 28. Implement strStr()
```python
class Solution:
    def strStr(self, haystack: str, needle: str) -> int:
        if not needle: return 0
        if needle not in haystack: return -1
        return haystack.index(needle)
```
```python
class Solution:
    def strStr(self, haystack: str, needle: str) -> int:
        try:
            return haystack.index(needle)
        except:
            return -1
```

### 35. Search Insert Position
```python
class Solution:
    def searchInsert(self, nums: List[int], target: int) -> int:
        if target in nums:
            return nums.index(target)
        
        if nums[-1]<target:
            return len(nums)
        
        for i, j in enumerate(nums):
            if j>target:
                return i
```

### 58. Length of Last Word
```python
class Solution:
    def lengthOfLastWord(self, s: str) -> int:
        s=s.rstrip()
        if len(s)==0:
            return 0
        out=0
        for char in s[::-1]:
            if char!=" ":
                out+=1
            else:
                return out
        return out
```
```python
class Solution:
    def lengthOfLastWord(self, s: str) -> int:
        return len(s.strip().split(' ')[-1])
```

### 66. Plus One
```python
class Solution:
    def plusOne(self, digits: List[int]) -> List[int]:
        digits[-1]=carry=digits[-1]+1
        i=-1
        maxlength=-1*len(digits)
        while carry==10 and i>=maxlength:
            digits[i]=0
            i-=1
            if i<maxlength:
                digits=[1]+digits
                return digits
            carry=digits[i]+1
            digits[i]+=1
        return digits
            
```

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
```python
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

### 1556. Thousand Separator
```python
class Solution:
    def thousandSeparator(self, n: int) -> str:
        char = str(n)[::-1]
        out = ""
        for i in range(0, len(char), 3):
            out += char[i:i+3] + "."
        return out[::-1][1:]
```
```python
class Solution:
    def thousandSeparator(self, n: int) -> str:
        s = str(n)
        out = []
        while s:
            out.append(s[-3:])
            s = s[:-3]
        return '.'.join(out[::-1])
```


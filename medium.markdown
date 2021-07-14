## **Other Python Practices - Medium**  

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

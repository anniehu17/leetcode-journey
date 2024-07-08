# Contains Duplicate
```
class Solution:
    def containsDuplicate(self, nums: List[int]) -> bool:
        seen = set()
        for num in nums:
            if num in seen:
                return True
            seen.add(num)
```
Note: none

# Valid Anagram
```
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        alphabet = [0] * 26

        for char in s:
            alphabet[ord(char) - ord('a')] += 1

        for char in t:
            alphabet[ord(char) - ord('a')] -= 1

        for i in range(len(alphabet)):
            if alphabet[i] != 0:
                return False
        
        return True
```
Note: usage of ord and [0] * 26 to create a size 26 array

# 217. Contains Duplicate
```python
class Solution:
    def containsDuplicate(self, nums: List[int]) -> bool:
        seen = set()
        for num in nums:
            if num in seen:
                return True
            seen.add(num)
```
Note: none

# 242. Valid Anagram
```python
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

# 1. Two Sum
```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        for i in range(len(nums)):
            for j in range(i + 1, len(nums)):
                if target - nums[i] == nums[j]:
                    return (i, j)
        
        return (0, 0)
```
Note: a better way is the below solution which is a one-pass hashmap
```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        hashmap = {}
        for i in range(len(nums)):
            complement = target - nums[i]
            if complement in hashmap:
                return [i, hashmap[complement]]
            hashmap[nums[i]] = i
```

# 49. Group Anagrams
```python
class Solution:
    def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
        ans = collections.defaultdict(list)
        for s in strs:
            ans[tuple(sorted(s))].append(s)
        return ans.values()
```
Note: usage of collections.defaultdict(list) and tuple(sorted(s)) to sort a string by its letters alphabetically
```python
class Solution:
    def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
        ans: DefaultDict[int, List[str]] = collections.defaultdict(list)
        for s in strs:
            count = [0] * 26
            for c in s:
                count[ord(c) - ord("a")] += 1
            ans[tuple(count)].append(s)
        return ans.values()
```
Note: converts each string to a unique count of its letters - usage of ans.values() to return only values of dict

# 347. Top K Frequent Elements
```python
class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        frequency = collections.defaultdict(int)

        for num in nums:
            frequency[num] += 1

        most_frequent = [(freq, elem) for elem, freq in frequency.items()]

        most_frequent.sort(reverse=True, key=lambda x: x[0])

        ans = list()
        for i in range(k):
            ans.append(most_frequent[i][1])
        
        return ans
```
Note: usage of lambda to sort and reversing a dict

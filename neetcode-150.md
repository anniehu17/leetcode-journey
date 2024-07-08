# Arrays & Hashing
## 217. Contains Duplicate
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

## 242. Valid Anagram
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

## 1. Two Sum
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

## 49. Group Anagrams
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

## 347. Top K Frequent Elements
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

## 271. Encode and Decode Strings
```python
class Codec:
    def encode(self, strs):
        # Initialize an empty string to hold the encoded string.
        encoded_string = ''
        for s in strs:
            # Append the length, the delimiter, and the string itself.
            encoded_string += str(len(s)) + '/:' + s
        return encoded_string

    def decode(self, s):
        # Initialize a list to hold the decoded strings.
        decoded_strings = []
        i = 0
        while i < len(s):
            # Find the delimiter.
            delim = s.find('/:', i)
            # Get the length, which is before the delimiter.
            length = int(s[i:delim])
            # Get the string, which is of 'length' length after the delimiter.
            str_ = s[delim+2 : delim+2+length]
            # Add the string to the list.
            decoded_strings.append(str_)
            # Move the index to the start of the next length.
            i = delim + 2 + length
        return decoded_strings
```
Note: possible algorithms include a non-ASCII delimiter, ecsaping an ASCII delimiter, and chunked transfer encoding (above)
## 238. Product of Array Except Self
```python
class Solution:
    def productExceptSelf(self, nums: List[int]) -> List[int]:
        prefix_products = [1] * len(nums)
        postfix_products = [1] * len(nums)

        for i in range(1, len(nums)):
            prefix_products[i] = prefix_products[i-1] * nums[i-1]

        for i in range(len(nums) - 2, -1, -1):
            postfix_products[i] = postfix_products[i+1] * nums[i+1]

        ans = [1] * len(nums)

        for i in range(len(nums)):
            ans[i] = prefix_products[i] * postfix_products[i]

        return ans
```
Note: example of backwards iteration of loop in p3

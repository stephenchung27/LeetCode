# 520. Detect Capital

- Difficulty: Easy
- [Link to Problem](https://leetcode.com/problems/detect-capital/)

## Notes

### First Thoughts

Since the input is a string with no additional knowledge on its contents, I know that I will have to iterate through it and check if each character is capitalized. This will take `O(n)` time complexity.

Since the output is a boolean, this leads me to believe that there can be a way to utilize simple conditionals each step, to get the correct answer in the end. This is only take up `O(1)` space.

Since the `ord` of capital letters live between the range of "A" and "Z", I can use that as an easy way to check if a character is capitalized.

### Code

```python
class Solution:
    def detectCapitalUse(self, word: str) -> bool:
        capitals = range(ord("A"), ord("Z") + 1)
        
        capitalized = False
        
        for index, char in enumerate(word):
            if index == 0 and ord(char) in capitals:
                capitalized = True
                continue
            elif capitalized and index == 1 and ord(char) not in capitals:
                capitalized = False
                continue
                
            if (capitalized and ord(char) not in capitals) or \
               (not capitalized and ord(char) in capitals):
                return False
            
        return True
```

### Solution

We can utilize Python's `all` built-in method to create a simple "one"-liner.
```python
class Solution:
    def detectCapitalUse(self, word: str) -> bool:
        return all(char == char.lower() for char in word) or \
               all(char == char.upper() for char in word) or \
               (word[0] == word[0].upper() and all(char == char.lower() for char in word[1:]))
```

Going even further, we can use Python's built-in string methods to create a true one-liner.
```python
class Solution:
    def detectCapitalUse(self, word: str) -> bool:
        return word.isupper() or word.islower() or word.istitle()
```

Here is a clever method using `min` and `max`:
```python
class Solution:
    def detectCapitalUse(self, word: str) -> bool:
        if len(word) < 2: return True
        if ord(word[0]) < 97:
            word = word[1:]
            return ord(max(word)) < 97 or ord(min(word)) >= 97
        else:
            return ord(min(word)) >= 97
```
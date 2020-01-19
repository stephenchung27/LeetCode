# 1108. Defanging an IP Address

- Difficulty: Easy
- [Link to Problem](https://leetcode.com/problems/defanging-an-ip-address/)

## Notes

### First Thoughts

Since I'm given an input where the location of the periods aren't obvious beforehand, I know that I will have to iterate through each character in the string to find each period. This will take `O(n)` time complexity.

Now, after finding a period, I can either make the change in-place or create another variable to hold the new string. The in-place option will allow `O(1)` space complexity, while the new string method will make it `O(n)` where `n` is the length of the string.

### Code

```python 3
class Solution:
    def defangIPaddr(self, address: str) -> str:
        ip = ""
        for char in address:
            if char == ".":
                ip = ip + "[.]"
            else:
                ip = ip + char
        return ip
```

### Solution

A very useful built-in function of string is `replace`. [Documentation](https://docs.python.org/2/library/string.html#string.replace)

> string.replace(s, old, new[, maxreplace])
>
> Return a copy of string s with all occurrences of substring old replaced by new. If the optional argument maxreplace is given, the first maxreplace occurrences are replaced.

Since the function is built-in and most likely optimized, we can use this to both shorten the length of the code and make it faster, albeit only marginally.

```python 3
class Solution:
  def defangIPadd(self, address: str) -> str:
    return address.replace(".", "[.]")
```
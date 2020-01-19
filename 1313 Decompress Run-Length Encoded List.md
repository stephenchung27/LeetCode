# 1313. Decompress Run-Length Encoded List

- Difficulty: Easy
- [Link to Problem](https://leetcode.com/problems/decompress-run-length-encoded-list/)

## Notes

### First Thoughts

The problem is poorly worded but basically it's asking us the take every odd index and add it to another array it's left-adjacent number of times.

Since it's dealing with a pair of things, I thought of using the `zip` keyword to "zip" the even and odd indices together.

Then using somthing along the lines of `[number] * times` to create an array and then concatenating them. If I used list comprehension, then we can possibly use the unpack `*[1, 2, 3]` operator to make it a one-liner!

### Code

In the interest of creating a single-liner, I came up with this.
```python
class Solution:
    def decompressRLElist(self, nums: List[int]) -> List[int]:
        return [ *([num]*times) for num, times in zip(nums[1::2], nums[::2])]
```
But was met with an error I've never seen before.
> Line 3: SyntaxError: iterable unpacking cannot be used in comprehension

Searching online, I found out that iterable unpacking is not available within list comprehension. It's only available in calls and when using assignments.

```python 3
class Solution:
    def decompressRLElist(self, nums: List[int]) -> List[int]:
        return [ x for num, times in zip(nums[1::2], nums[::2]) for x in [num]*times ]
```

Eventually came up with this using two for loops. It's very unintuitive how the inner loop is placed towards the outside when using list comprehension. You would think going closer to `x` would be deeper into the nested loops.


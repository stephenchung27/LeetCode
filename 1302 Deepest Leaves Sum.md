# 1302. Deepest Leaves Sum

- Difficulty: Medium
- [Link to Problem](https://leetcode.com/problems/deepest-leaves-sum/)

## Notes

### First Thoughts

So, just spitting off my initial thoughts, I can always do dfs/bfs and pass down the current depth within the binary tree.

If using bfs, I would have to use an array that kept track of the running sum of each level.

When using dfs, I could pass in the depth with the node into the queue, allowing me to keep just a single variable to keep track of the sum and reset it once the depth changes, since we're really only interested in the very bottom row.

Since dfs/bfs both have the same time complexity (I would have to traverse every node because we have no additional information on what's within the tree, so `O(n)`) I chose to go with the marginally better (`O(n)` as opposed to `O(2n)`) bfs.

### Code

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

from collections import deque

class Solution:
    def deepestLeavesSum(self, root: TreeNode) -> int:
        maxDepth = 0
        q = deque([(root, 0)])
        total = 0

        while q:
            node, depth = q.popleft() # Unpack the tuple!

            if not node: continue

            if depth > maxDepth:
                maxDepth = depth
                total = 0 # Reset the sum since we're at a new depth now
            
            total = total + node.val

            q.append((node.left, depth + 1)) # Make sure to add the depth when appended to the queue
            q.append((node.right, depth + 1))
    
        return total
```

[Documentation on `deque`](https://docs.python.org/2/library/collections.html#collections.deque)
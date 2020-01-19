# 1315. Sum of Nodes with Even-Valued Grandparent

- Difficulty: Medium
- [Link to Problem](https://leetcode.com/problems/sum-of-nodes-with-even-valued-grandparent/)

## Notes

### First Thoughts

My first thought is to use a nested function that keeps track of the parent and grandparent. Within each recursive call, the next call would push the node's parent to the grandparent spot and place it's own value to the parent spot when calling itself of the children nodes.

Meanwhile, there would be a sum variable that lives outside of the function that gets added onto everytime the grandparent is even. 

Now that I think about it, we really don't even need to pass down a grandparent value because, if within the current node, the parent is an even value, then we can just add it's children's values to the sum.

### Code

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def sumEvenGrandparent(self, root: TreeNode) -> int:
        totalSum = [0]
        
        def recurse(node, parent):
            if not node: return
            
            if parent and parent.val % 2 == 0:
                totalSum[0] =   totalSum[0] \
                              + (node.left.val if node.left else 0) \
                              + (node.right.val if node.right else 0)
            
            recurse(node.left, node)
            recurse(node.right, node)
        
        recurse(root, None)
        
        return totalSum[0]
```

Now this solution works, but I wanted to practice not using a nested function for these types of problems. Also, using an array to bypass the nested function assignment seems hacky and would not fly within a team with good coding practices.

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def sumEvenGrandparent(self, root: TreeNode, parent: TreeNode = None) -> int:
        if not root: return 0
        
        totalSum = 0
        
        if parent and parent.val % 2 == 0:
            totalSum =   totalSum \
                       + (root.left.val if root.left else 0) \
                       + (root.right.val if root.right else 0)
        
        totalSum =   totalSum \
                   + self.sumEvenGrandparent(root.left, root) \
                   + self.sumEvenGrandparent(root.right, root)
        
        return totalSum
```

Also discovered a solution using the `nonlocal` keyword which initializes a variable that can be used outside of it's scope!

```python
class Solution:
    def sumEvenGrandparent(self, root: TreeNode) -> int:
        
        def dfs(node: TreeNode, parent: TreeNode, grandParent: TreeNode):
            if not node:
                return
            nonlocal answer
            if parent and grandParent and grandParent.val % 2 == 0:
                answer += node.val
            dfs(node.left, node, parent)
            dfs(node.right, node, parent)

        answer = 0
        dfs(root, None, None)
        return answer
```
# 144. 前序遍历

我的是最优解吗？: No
最优解分析了吗？: Yes
自己做出来了吗？: No

```python
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def preorderTraversal(self, root: TreeNode):
        # end condition:the value of a node is "None"
        # argument: 根root
        # return: preorderTraversal(root.val), preorderTraversal(root.left) preorderTraversal(root.right)
        ans = []
        
        def traversal(root):
            if root == None:
                return
            ans.append(root.val)
            traversal(root.left)
            traversal(root.right)

        traversal(root)
        return ans
```

终止条件有点混淆，我之前以为是 `root.left == None and root.right == None`的时候才跳出去。

![Untitled](144%20%E5%89%8D%E5%BA%8F%E9%81%8D%E5%8E%86%20afb0e2dc7ffa442ca0c2df08e4c24707/Untitled.png)

<img src="144%20%E5%89%8D%E5%BA%8F%E9%81%8D%E5%8E%86%20afb0e2dc7ffa442ca0c2df08e4c24707/Untitled%201.png" alt="Untitled" style="zoom: 25%;" />

在递归的过程中，如何算是递归结束了呢，当然是当前遍历的节点是空了，那么本层递归就要要结束了，所以如果当前遍历的这个节点是空，就直接return。而如果当前已经为空，还去找左右孩子，会报错。

比如上图，如果是`root.left == None and root.right == None`的判断条件，1的左孩子为空但右孩子非空，则递归到`traversal(root.left)` ，就会发现此时左孩子已空，还找左右孩子就会报错。
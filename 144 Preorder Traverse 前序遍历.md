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

![image](https://user-images.githubusercontent.com/104201605/182763445-d8acf8e9-d2f9-470e-94fe-0f8a594f9a08.png)

![无标题](https://user-images.githubusercontent.com/104201605/182764496-e89a2907-c7e6-4a8d-bdbf-f7e56ec2a24a.png)

在递归的过程中，如何算是递归结束了呢，当然是当前遍历的节点是空了，那么本层递归就要要结束了，所以如果当前遍历的这个节点是空，就直接return。而如果当前已经为空，还去找左右孩子，会报错。

比如上图，如果是`root.left == None and root.right == None`的判断条件，1的左孩子为空但右孩子非空，则递归到`traversal(root.left)` ，就会发现此时左孩子已空，还找左右孩子就会报错。

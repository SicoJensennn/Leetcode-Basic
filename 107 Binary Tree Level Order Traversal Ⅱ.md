# 107. Binary Tree Level Order Traversal Ⅱ

我的是最优解吗？: Yes
最优解分析了吗？: No
自己做出来了吗？: Yes

I used 2 methods to solve this out.

- The first one is BFS + reverse.
    
    ```python
    ans = []
            if root is None:
                return ans
    
            que = deque()
            que.append(root)
            while len(que) > 0:
                lis = []
                size = len(que)
                while size > 0:
                    temp = que.popleft()
                    lis.append(temp.val)
                    if temp.left != None:
                        que.append(temp.left)
                    if temp.right != None:
                        que.append(temp.right)
                    size -= 1
                ans.append(lis[:])
            ans.reverse()
            return ans
    ```
    

The second one is DFS. I don’t wanna use reverse again, so I set the level, the first layer can be added to the last list. However, we need to know the depth of binary tree thus can we gain the level. So, I wrote another function named depth. 

```python
ans = []
        if root == None:
            return ans
        deep = self.depth(root, 0)
        for i in range(deep):
            ans.append([])
        self.dfs(ans, root, deep)
        return ans

    def dfs(self, ans, root, level):
        if root == None:
            return ans
        ans[level - 1].append(root.val)  # level - 1, or the list will out of range

        if root.left != None:
            self.dfs(ans, root.left, level - 1)
        if root.right != None:
            self.dfs(ans,  root.right, level - 1)

    def depth(self, root, dep):
        if root == None:
            return dep
        dep += 1
        left = self.depth(root.left,dep)
        right = self.depth(root.right,dep)
        return max(left, right)
```
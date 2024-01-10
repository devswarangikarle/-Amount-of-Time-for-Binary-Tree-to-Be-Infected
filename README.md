# -Amount-of-Time-for-Binary-Tree-to-Be-Infected
You are given the root of a binary tree with unique values, and an integer start. At minute 0, an infection starts from the node with value start.  Each minute, a node becomes infected if:  The node is currently uninfected. The node is adjacent to an infected node. Return the number of minutes needed for the entire tree to be infected.


class Solution:
    def amountOfTime(self, root: Optional[TreeNode], start: int) -> int:
        graph=defaultdict(list)
        stack=[(root,None)]
        while stack:
            n,p=stack.pop()
            if p:
                graph[p.val].append(n.val)
                graph[n.val].append(p.val)
            if n.left:
                stack.append((n.left,n))
            if n.right:
                stack.append((n.right,n))
        ans=-1
        seen={start}
        queue=deque([start])
        while queue:
            for _ in range(len(queue)):
                u=queue.popleft()
                for v in graph[u]:
                    if v not in seen:
                        seen.add(v)
                        queue.append(v)
            ans+=1
        return ans                                

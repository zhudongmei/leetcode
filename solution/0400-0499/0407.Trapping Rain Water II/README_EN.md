# [407. Trapping Rain Water II](https://leetcode.com/problems/trapping-rain-water-ii)

[中文文档](/solution/0400-0499/0407.Trapping%20Rain%20Water%20II/README.md)

## Description

<p>Given an <code>m x n</code> integer matrix <code>heightMap</code> representing the height of each unit cell in a 2D elevation map, return <em>the volume of water it can trap after raining</em>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<img alt="" src="https://fastly.jsdelivr.net/gh/doocs/leetcode@main/solution/0400-0499/0407.Trapping%20Rain%20Water%20II/images/trap1-3d.jpg" style="width: 361px; height: 321px;" />
<pre>
<strong>Input:</strong> heightMap = [[1,4,3,1,3,2],[3,2,1,3,2,4],[2,3,3,2,3,1]]
<strong>Output:</strong> 4
<strong>Explanation:</strong> After the rain, water is trapped between the blocks.
We have two small ponds 1 and 3 units trapped.
The total volume of water trapped is 4.
</pre>

<p><strong class="example">Example 2:</strong></p>
<img alt="" src="https://fastly.jsdelivr.net/gh/doocs/leetcode@main/solution/0400-0499/0407.Trapping%20Rain%20Water%20II/images/trap2-3d.jpg" style="width: 401px; height: 321px;" />
<pre>
<strong>Input:</strong> heightMap = [[3,3,3,3,3],[3,2,2,2,3],[3,2,1,2,3],[3,2,2,2,3],[3,3,3,3,3]]
<strong>Output:</strong> 10
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>m == heightMap.length</code></li>
	<li><code>n == heightMap[i].length</code></li>
	<li><code>1 &lt;= m, n &lt;= 200</code></li>
	<li><code>0 &lt;= heightMap[i][j] &lt;= 2 * 10<sup>4</sup></code></li>
</ul>

## Solutions

<!-- tabs:start -->

### **Python3**

```python
class Solution:
    def trapRainWater(self, heightMap: List[List[int]]) -> int:
        m, n = len(heightMap), len(heightMap[0])
        vis = [[False] * n for _ in range(m)]
        pq = []
        for i in range(m):
            for j in range(n):
                if i == 0 or i == m - 1 or j == 0 or j == n - 1:
                    heappush(pq, (heightMap[i][j], i, j))
                    vis[i][j] = True

        ans = 0
        while pq:
            e = heappop(pq)
            for x, y in [[0, 1], [0, -1], [1, 0], [-1, 0]]:
                i, j = e[1] + x, e[2] + y
                if i >= 0 and i < m and j >= 0 and j < n and not vis[i][j]:
                    if heightMap[i][j] < e[0]:
                        ans += e[0] - heightMap[i][j]
                    vis[i][j] = True
                    heappush(pq, (max(heightMap[i][j], e[0]), i, j))
        return ans
```

### **Java**

```java
class Solution {
    public int trapRainWater(int[][] heightMap) {
        int m = heightMap.length, n = heightMap[0].length;
        boolean[][] vis = new boolean[m][n];
        PriorityQueue<int[]> pq = new PriorityQueue<>((o1, o2) -> o1[0] - o2[0]);
        for (int i = 0; i < m; ++i) {
            for (int j = 0; j < n; ++j) {
                if (i == 0 || i == m - 1 || j == 0 || j == n - 1) {
                    pq.offer(new int[] {heightMap[i][j], i, j});
                    vis[i][j] = true;
                }
            }
        }
        int ans = 0;
        int[][] dirs = new int[][] {{0, -1}, {0, 1}, {1, 0}, {-1, 0}};
        while (!pq.isEmpty()) {
            int[] e = pq.poll();
            for (int[] d : dirs) {
                int i = e[1] + d[0], j = e[2] + d[1];
                if (i >= 0 && i < m && j >= 0 && j < n && !vis[i][j]) {
                    if (heightMap[i][j] < e[0]) {
                        ans += e[0] - heightMap[i][j];
                    }
                    vis[i][j] = true;
                    pq.offer(new int[] {Math.max(heightMap[i][j], e[0]), i, j});
                }
            }
        }
        return ans;
    }
}
```

### **...**

```

```

<!-- tabs:end -->

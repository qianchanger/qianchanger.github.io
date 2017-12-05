---
date: 2017-12-05
layout: post
title: "[JobHunt]leetcode - Number of Islands "
categories: code
tags: leetcode
---

https://leetcode.com/problems/number-of-islands/description/   
这属于一类经典走matrix的题目   
其关键是要给走过的地方加一个记号   
然后每遇到一个可以走的地方 就使用BFS/DFS走穿(走到不能再走)就行了   
时间复杂度是O(M*N) M和N是矩阵的长度和宽度 因为每个点其实就走了1次   

<!--more-->

{% highlight python %}
    def numIslands(self, grid):
        """
        :type grid: List[List[str]]
        :rtype: int
        """        
        if not grid:
            return 0

        def expand_island(start_point, grid):
            """
            :type start_point: (int, int) , the starting point
            :type grid: List[List[str]]
            """
            vertical_len = len(grid)
            horizontal_len = len(grid[0])
            
            queue = [start_point]
            while queue:
                x, y = queue.pop()
                # looks around - up
                if x-1 >= 0 and grid[x-1][y] == '1':
                    queue.append((x-1, y))
                # look around - left
                if y-1 >= 0 and grid[x][y-1] == '1':
                    queue.append((x, y-1))
                # look around - below
                if x+1 < vertical_len and grid[x+1][y] == '1':
                    queue.append((x+1, y))
                # lok around - right
                if y+1 < horizontal_len and grid[x][y+1] == '1':
                    queue.append((x, y+1))
                # mark the processed bit as travelled
                grid[x][y] = '*'
                
        island_count = 0
        for x in range(len(grid)):
            for y in range(len(grid[0])):
                if grid[x][y] == '1':
                    island_count += 1
                    expand_island((x,y), grid)
        return island_count
{% endhighlight %}


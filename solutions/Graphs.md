# Graphs-
This file contains all the solutions of the graphs questions of algomap leetcode sheet.
Language used-C++

## 1.Find if path exists in graph-
**Link:** https://leetcode.com/problems/find-if-path-exists-in-graph/description/

class Solution 
{
public:
    bool validPath(int n, vector<vector<int>>& edges, int source, int destination) 
    {
       int n1=edges.size();
       vector<vector<int>>list(n);
       for(auto &e:edges)
       {
        int u=e[0],v=e[1];
        list[u].push_back(v);
        list[v].push_back(u);
       }
      vector<bool>visited(n,false);
      queue<int>q;
      q.push(source);
      visited[source]=true;
      while(!q.empty())
      {
        int cv=q.front();
        q.pop();
         if(cv==destination)
                return true;
        for(int i:list[cv])
        {
            if(visited[i]==false)
            {
                q.push(i);
                visited[i]=true;
            }
        }
      }
      return false;
    }
};



## 2.Number of islands-
**Link:** https://leetcode.com/problems/number-of-islands/description/

class Solution 
{
public:
void dfs(vector<vector<char>>& grid, int i, int j) 
{
        int m = grid.size();
        int n = grid[0].size();
        if (i < 0 || i >= m || j < 0 || j >= n || grid[i][j] != '1') 
        return;
        grid[i][j] = '0';
        dfs(grid, i, j + 1);
        dfs(grid, i + 1, j);
        dfs(grid, i, j - 1);
        dfs(grid, i - 1, j);
}
    int numIslands(vector<vector<char>>& grid) 
    {
        if (grid.empty() || grid[0].empty())
        return 0;
        int m = grid.size();
        int n = grid[0].size();
        int numIslands = 0;
        for (int i = 0; i < m; ++i) 
        {
            for (int j = 0; j < n; ++j) 
            {
                if (grid[i][j] == '1') 
                {
                    numIslands++;
                    dfs(grid, i, j);
                }
            }
        }
        return numIslands;
    }
};



## 3.Max area of island-
**Link:** https://leetcode.com/problems/max-area-of-island/description/

class Solution 
{
public:
int dfs(vector<vector<int>>&grid,int i,int j,int &count)
{
    int m=grid.size();
    int n=grid[0].size();
    if(i<0 || i>(m-1) || j<0 || j>(n-1) || grid[i][j]!=1)
    return 0;
    count++;
    grid[i][j]=0;
    dfs(grid,i,j+1,count);
    dfs(grid,i,j-1,count);
    dfs(grid,i+1,j,count);
    dfs(grid,i-1,j,count);
    return count;
}
    int maxAreaOfIsland(vector<vector<int>>& grid) 
    {
        if(grid.empty() || grid[0].empty())
        return 0;
        int m=grid.size();
        int n=grid[0].size();
        int count;
        int maxi=0;
        for(int i=0;i<m;i++)
        {
            for(int j=0;j<n;j++)
            {
                if(grid[i][j]==1)
                {
                    count=0;
                    dfs(grid,i,j,count);  
                    maxi=max(maxi,count);
                }
            }
        }
      return maxi;
    }
};



## 4.Course schedule(Detecting cycles in a graph)-
**Link:** https://leetcode.com/problems/course-schedule/description/

class Solution 
{
public:
    bool canFinish(int numCourses, vector<vector<int>>& prerequisites) 
    {
        int u,v;
        vector<int>indegree(numCourses,0);
        vector<vector<int>>list(numCourses);
        if(numCourses==1 || prerequisites.empty())
        {
         return true;
        }
        int j=0;
        for(auto a:prerequisites)
        {
            u=a[0],v=a[1];
            indegree[u]++;
            list[v].push_back(u);
        }
        int count=0;
        queue<int>q;
        for(int i=0;i<numCourses;i++)
        {
        if(indegree[i]==0)
        {
            q.push(i);
        }
        }
        if(q.empty())
        return false;
        else 
        {
        while(!q.empty())
        {
            int x=q.front();
            q.pop();
            count++;
            for(int i:list[x])
            {
            indegree[i]--;
            if(indegree[i]==0)
            {
                q.push(i);
            }
            }
        }
        }
        return count==numCourses;
    }
};



## 5.Course schedule 2(Topological sort)-
**Link:** https://leetcode.com/problems/course-schedule-ii/description/

class Solution 
{
public:
    vector<int> findOrder(int numCourses, vector<vector<int>>& prerequisites) 
    {
        vector<int>indegree(numCourses,0);
        vector<vector<int>>list(numCourses);
        vector<int>ans;
        if(numCourses==1)
        {
            ans.push_back(0);
            return ans;
        }
        if(prerequisites.empty())
        {
            for(int i=numCourses-1;i>=0;i--)
            {
                ans.push_back(i);
            }
            return ans;
        }
        for(auto a:prerequisites)
        {
            int u=a[0],v=a[1];
            indegree[u]++;
            list[v].push_back(u);
        }
        int j=0;
        queue<int>q;
        int count=0;
        for(int i=0;i<numCourses;i++)
        {
            if(indegree[i]==0)
            {
                q.push(i);
            }
        }
        if(q.empty())
        return ans;
        while(!q.empty())
        {
            int x=q.front();
            q.pop();
            count++;
            ans.push_back(x);
            for(int i:list[x])
            {
                indegree[i]--;
                if(indegree[i]==0)
                {
                    q.push(i);
                }
            }
        }
        if(count==numCourses)
        {
        return ans;
        }
        else 
        {
            return {};
        }
    }
};



## 6.Pacific atlantic water flow-
**Link:** https://leetcode.com/problems/pacific-atlantic-water-flow/description/

class Solution 
{
public:
    int m, n;
    vector<vector<int>> directions = {{1, 0}, {-1, 0}, {0, 1}, {0, -1}};    
    void dfs(vector<vector<int>>& heights, int i, int j, vector<vector<bool>>& ocean) 
    {
        ocean[i][j] = true;
        for (auto dir : directions) 
        {
            int ni = i + dir[0];
            int nj = j + dir[1];
            if (ni < 0 || nj < 0 || ni >= m || nj >= n) continue;
            if (ocean[ni][nj]) 
            continue;
            if (heights[ni][nj] < heights[i][j]) 
            continue;
            dfs(heights, ni, nj, ocean);
        }
    }
    vector<vector<int>> pacificAtlantic(vector<vector<int>>& heights) 
    {
        m = heights.size();
        n = heights[0].size();
        vector<vector<bool>> pacific(m, vector<bool>(n, false));
        vector<vector<bool>> atlantic(m, vector<bool>(n, false));    
        for (int i = 0; i < m; ++i) 
        {
            dfs(heights, i, 0, pacific);        
            dfs(heights, i, n - 1, atlantic);    
        }
        for (int j = 0; j < n; ++j) 
        {
            dfs(heights, 0, j, pacific);         
            dfs(heights, m - 1, j, atlantic);    
        }
        vector<vector<int>> result;
        for (int i = 0; i < m; ++i) 
        {
            for (int j = 0; j < n; ++j) 
            {
                if (pacific[i][j] && atlantic[i][j]) 
                {
                    result.push_back({i, j});
                }
            }
        }
        return result;
    }
};



## 7.Rotting oranges-
**Link:** https://leetcode.com/problems/rotting-oranges/description/

class Solution 
{
public:
    int orangesRotting(vector<vector<int>>& grid) 
    {
        int m = grid.size(), n = grid[0].size();
        queue<pair<pair<int, int>, int>> q;
        vector<vector<int>> visited(m, vector<int>(n, 0));
        
        int freshCount = 0;
        for (int i = 0; i < m; ++i) 
        {
            for (int j = 0; j < n; ++j) 
            {
                if (grid[i][j] == 2) 
                {
                    q.push({{i, j}, 0});
                    visited[i][j] = 1;
                }
                else if (grid[i][j] == 1) 
                {
                    freshCount++;
                }
            }
        }

        int maxTime = 0;
        vector<vector<int>> dir = {{0,1}, {0,-1}, {1,0}, {-1,0}};

        while (!q.empty()) {
            auto front = q.front(); q.pop();
            int i = front.first.first;
            int j = front.first.second;
            int time = front.second;
            maxTime = max(maxTime, time);

            for (auto d : dir) 
            {
                int ni = i + d[0];
                int nj = j + d[1];

                if (ni >= 0 && nj >= 0 && ni < m && nj < n &&
                    grid[ni][nj] == 1 && !visited[ni][nj]) 
                    {
                    grid[ni][nj] = 2;
                    visited[ni][nj] = 1;
                    q.push({{ni, nj}, time + 1});
                    freshCount--;
                }
            }
        }

        return (freshCount == 0) ? maxTime : -1;
    }
};


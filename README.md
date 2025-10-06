# 778-swim-in-rising-water
daily leetcode challange 
class Solution {
public:
    int swimInWater(vector<vector<int>>& grid) {
        int n = grid.size();
        vector<vector<int>> dirs = {{1,0}, {-1,0}, {0,1}, {0,-1}};
        vector<vector<bool>> visited(n, vector<bool>(n, false));
        priority_queue<vector<int>, vector<vector<int>>, greater<vector<int>>> pq;
        pq.push({grid[0][0], 0, 0});
        visited[0][0] = true;
        
        while (!pq.empty()) {
            auto top = pq.top();
            pq.pop();
            int elevation = top[0];
            int r = top[1];
            int c = top[2];
            
            if (r == n-1 && c == n-1) return elevation;
            
            for (auto &d : dirs) {
                int nr = r + d[0];
                int nc = c + d[1];
                
                if (nr >= 0 && nr < n && nc >= 0 && nc < n && !visited[nr][nc]) {
                    visited[nr][nc] = true;
                    pq.push({max(elevation, grid[nr][nc]), nr, nc});
                }
            }
        }
        
        return -1;
    }
};


You are given an integer n, which indicates that there are n courses labeled from 1 to n. You are also given an array relations where relations[i] = [prevCoursei, nextCoursei], representing a prerequisite relationship between course prevCoursei and course nextCoursei: course prevCoursei has to be taken before course nextCoursei.

In one semester, you can take any number of courses as long as you have taken all the prerequisites in the previous semester for the courses you are taking.

Return the minimum number of semesters needed to take all courses. If there is no way to take all the courses, return -1.



Example 1:

![img.png](img.png)


Input: n = 3, relations = [[1,3],[2,3]]
Output: 2
Explanation: The figure above represents the given graph.
In the first semester, you can take courses 1 and 2.
In the second semester, you can take course 3.


### Approach 1 : BFS
```
class Solution {
    public int minimumSemesters(int n, int[][] relations) {
        
        int[] inCount = new int[n + 1]; // or indegree
        List<List<Integer>> graph = new ArrayList<>(n + 1);
        for (int i = 0; i < n + 1; ++i) {
            graph.add(new ArrayList<Integer>());
        }
        for (int[] relation : relations) {
            graph.get(relation[0]).add(relation[1]);
            inCount[relation[1]]++;
        }
        
        int step = 0;
        int studiedCount = 0;
        Queue<Integer> q = new LinkedList<>();
        
        for(int i = 1;i < n+1;i++){
            if(inCount[i] == 0)
                q.add(i);
        }
        
        while(!q.isEmpty()){
            step++;
            Queue<Integer> nextQ = new LinkedList<>();
            for(int node : q){
                studiedCount++;
                for(int endNode : graph.get(node)){
                    if(--inCount[endNode] == 0)
                        nextQ.add(endNode);
                }
            }
            
            q = nextQ;
        }
        
        return studiedCount == n ? step : -1;
        
    }
}
```


### DFS  - Check longest Path, without cycles
![img_1.png](img_1.png)
```

```

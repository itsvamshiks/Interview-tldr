##Optimized Disjoint set implementation for

```

class UnionFind { 

    private int[] root;
    // Use a rank array to record the height of each vertex, i.e., the "rank" of each vertex.
    private int[] rank;
    
    public UnionFind(int size){
        root = new int[size];
        rank = new int[size];
        for(int i = 0;i < size;i++){
            root[i] = i;
            rank[i] = 1;
        }
    }
    
    public int find(int x){
        if(x == root[x])
            return x;
        return root[x] = find(root[x]);
    }
    
    public void union(int x,int y){
        int rootX = root[x];
        int rootY = root[y];
        
        if(rootX != rootY){
            if(rank[x] > rank[y]){
                root[rootY] = rootX;
            } else if(rank[x] < rank[y]){
                root[rootX] = rootY;
            } else{
                root[rootY] = rootX;
                rank[rootX] += 1;
            }
        }
    
    }
    
    public boolean connected(int x,int y){
        return find(x) == find(y);
    }

}

// App.java
// Test Case

public class App {
    UnionFind uf = new UnionFind(10);
    uf.union(1,2);
    uf.union(2,5);
    uf.union(5, 6);
    uf.union(6, 7);
    uf.union(3, 8);
    uf.union(8, 9);
    
    System.out.println(uf.connected(1, 5)); // true
    System.out.println(uf.connected(5, 7)); // true
    System.out.println(uf.connected(4, 9)); // false
    
    uf.union(9, 4);
    System.out.println(uf.connected(4, 9)); // true

}


```

Time complexity : 

constructor = O(N);
find = union = connected = O(alpha(N));

alpha - ackermann function. On average, O(alpha(N)) = O(1);

Space complexity:
O(n)

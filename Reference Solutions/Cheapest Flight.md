## Cheapest Flight within k stops


```
 public int findCheapestPrice(int n, int[][] flights, int src, int dst, int k) {
        
        int[][] prices = new int[2][n];
        
        Arrays.fill(prices[0],Integer.MAX_VALUE);
        Arrays.fill(prices[1],Integer.MAX_VALUE);
        
        prices[0][src] = 0;
        prices[1][src] = 0;
        
        for(int i = 0;i <=k+1;i++){
            for(int[] flight: flights){
                int s = flight[0],d = flight[1],pSD = flight[2];
                
                int pS = prices[1-i&1][s];
                int pD = prices[i&1][d];
                if(pS < Integer.MAX_VALUE){
                    if(pS + pSD < pD){
                        prices[i&1][d] = pS + pSD;
                    }
                }
            }
        }
        
        return prices[k&1][dst]  == Integer.MAX_VALUE ? -1 : prices[k&1][dst];
 }

```

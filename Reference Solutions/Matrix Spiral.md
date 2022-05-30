Given an m x n matrix, return all elements of the matrix in spiral order.

![img_3.png](img_3.png)

```
class Solution {
    public List<Integer> spiralOrder(int[][] matrix) {
        
        List<Integer> result = new ArrayList<>();
        
        int rows = matrix.length;
        int cols = matrix[0].length;
        
        int up = 0,left = 0,down = rows-1,right = cols-1;
        
        while(result.size() < rows*cols){
            for(int i = left;i <= right;i++)
                result.add(matrix[up][i]);
            
            for(int i = up+1;i <= down;i++){
                result.add(matrix[i][right]);
            }
            
            if(up!=down){
                for(int i = right -1;i >= left;i--)
                    result.add(matrix[down][i]);
            }
            
            if(left!=right){
                for(int i = down - 1;i >up;i--){
                    result.add(matrix[i][left]);
                }
            }
            
            left++;
            right--;
            up++;
            down--;      
        }
        return result;
    }
}
```

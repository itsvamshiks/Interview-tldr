## Sort Colors 


Given an array nums with n objects colored red, white, or blue, sort them in-place so that objects of the same color are adjacent, with the colors in the order red, white, and blue.

We will use the integers 0, 1, and 2 to represent the color red, white, and blue, respectively.

You must solve this problem without using the library's sort function.


```

class Solution {
    public void sortColors(int[] nums) {
        
        int p0 = 0,curr = 0,p2 = nums.length -1;
        
        int tmp;
        
        while(curr <= p2){
            if(nums[curr] == 0){
                tmp = nums[p0];
                nums[p0++] = nums[curr];
                nums[curr++] = tmp;
            }else if(nums[curr] == 2){
                tmp = nums[p2];
                nums[p2--] = nums[curr];
                nums[curr] = tmp;
            }else
                curr++;
        }
        
        
    }
}

```

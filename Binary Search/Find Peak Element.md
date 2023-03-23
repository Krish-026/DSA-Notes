Given an array, we need to find the peak element.  
As, the subportions of the array are increasing/decreasing ( only then we would be able to find peak ), there are subportions of array which are sorted, so we could use binary search to get this problem done. But exactly how ?

This is an interesting part.

For a mid element, there could be three possible cases :  

![[Pasted image 20230323121938.png]]

Case 1 : mid lies on the right of our result peak ( Observation : Our peak element search space is leftside )  
Case 2 : mid is equal to the peak element ( Observation : mid element is greater than its neighbors )  
Case 3 : mid lies on the left. ( Observation : Our peak element search space is rightside )

so, the code becomes

```cpp
class Solution {
public:
    int findPeakElement(vector<int>& nums) {
        int l = 0, h = nums.size()-1, n = nums.size();
        while(l <= h){
            int mid = l + (h-l)/2;
            if((mid == l or nums[mid] > nums[mid-1]) 
               and (mid == h or nums[mid] > nums[mid+1]))
                return mid;
                else if(nums[mid+1] > nums[mid]) l = mid + 1;
                else h = mid - 1;
        }
        return -1;
    }
};
```
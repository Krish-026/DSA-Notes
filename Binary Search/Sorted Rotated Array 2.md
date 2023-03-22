

```cpp
class Solution {
public:
    bool search(vector<int>& nums, int target) {
        int n = nums.size();
        int l = 0, h = n-1;
        if(nums[l] == target or nums[h] == target) return true;
        while(l < h and nums[l] == nums[h]) ++l;
        while(l <= h){
            int mid = l + (h - l) / 2;
            if(nums[mid] == target)
                return true;
            else if(nums[l] <= nums[mid]){
                if(target >= nums[l] and target <= nums[mid])
                    h = mid - 1;
                else l = mid + 1;
            }
            else{
                if(target >= nums[mid] and target <= nums[h])
                     l = mid + 1;
                else h = mid - 1;
            }
        }
        return false;
    }
};
```
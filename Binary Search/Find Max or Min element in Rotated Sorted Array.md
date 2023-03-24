
-   (1) loop is `left < right`, which means inside the loop, `left` always < `right`
-   (2 ) since we use round up for `mid`, and `left < right` from (1), **`right` would never be the same as `mid`**
-   (3) Therefore, we compare `mid` with `right`, since they will never be the same from (2)
-   (4) if `nums[mid] < nums[right]`, we will know the minimum should be in the left part, so we are moving `right`.
    -   We can always make `right = mid` while we don't have to worry the loop will not ends. Since from (2), we know `right` would never be the same as `mid`, making `right = mid` will assure the interval is shrinking.
-   (5) if `nums[mid] > nums[right]`, minimum should be in the right part, so we are moving `left`. Since `nums[mid] > nums[right]`, `mid` can't be the minimum, we can safely move `left` to `mid + 1`, which also assure the interval is shrinking

class Solution {

public:

    int findMin(vector<int>& nums) {

        int l = 0, r = nums.size()-1, mid= (l + (r-l)/2);

        while(l < r){

            int mid = l + (r-l)/2;

            if(nums[mid] > nums[r])

                l = mid + 1;

            else

                r = mid;

        }

        return nums[l];

    }

};
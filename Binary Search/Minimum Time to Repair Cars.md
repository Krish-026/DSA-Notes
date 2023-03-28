#CST101-28-03-2023 
#28-03-2023 
[[Capacity To Ship Packages Within D Days]]


You are given an integer array `ranks` representing the **ranks** of some mechanics. ranksi is the rank of the ith mechanic. A mechanic with a rank `r` can repair n cars in `r * n2` minutes.

You are also given an integer `cars` representing the total number of cars waiting in the garage to be repaired.

Return _the **minimum** time taken to repair all the cars._

**Note:** All the mechanics can repair the cars simultaneously.

**Example 1:**

**Input:** ranks = `[4,2,3,1]`, cars = 10
**Output:** 16
**Explanation:** 
- The first mechanic will repair two cars. The time required is 4 * 2 * 2 = 16 minutes.
- The second mechanic will repair two cars. The time required is 2 * 2 * 2 = 8 minutes.
- The third mechanic will repair two cars. The time required is 3 * 2 * 2 = 12 minutes.
- The fourth mechanic will repair four cars. The time required is 1 * 4 * 4 = 16 minutes.
It can be proved that the cars cannot be repaired in less than 16 minutes.​​​​​

**Example 2:**

**Input:** ranks = `[5,1,8]`, cars = 6
**Output:** 16
**Explanation:** 
- The first mechanic will repair one car. The time required is 5 * 1 * 1 = 5 minutes.
- The second mechanic will repair four cars. The time required is 1 * 4 * 4 = 16 minutes.
- The third mechanic will repair one car. The time required is 8 * 1 * 1 = 8 minutes.
It can be proved that the cars cannot be repaired in less than 16 minutes.​​​​​

**Constraints:**

-   `1 <= ranks.length <= 105`
-   `1 <= ranks[i] <= 100`
-   `1 <= cars <= 106`



```cpp
class Solution {
private:
    bool isPossible(long long time, int cars, vector<int>&ranks){
        int t = 0, size = ranks.size();
        for(int i = 0; i < size; ++i){
            t = sqrt(time/ranks[i]);
            if(cars > 0){
                cars -= t;
            }
            else break;
        }
        return cars <= 0 ? true: false;
    }
public:
    long long repairCars(vector<int>& ranks, int cars) {
        long long l = 1, h = 0, ans = 0;
        for(int x: ranks) h = max((int)h, x);
        h = h * cars * cars;
        // l and h is min and max time
        while(l <= h){
            long long mid = l + (h-l)/2;
            if(isPossible(mid, cars, ranks)){
                ans = mid;
                h = mid - 1;
            }
            else l = mid + 1;
        }
        return ans;
    }
};
```
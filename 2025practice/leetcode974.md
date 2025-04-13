# 974. Subarray Sums Divisible by K

##  describtion
None

```C++
int subarraysDivByK(vector<int>& nums, int k) {
        vector<int>  pre(nums.size(), 0);
        unordered_map<int, int> map;
        map[0] = 1; // 考虑整除时需要主动加上
        int sum = 0, res = 0;
        for (int num : nums) {
            sum += num;
            int tmp = (sum % k + k) % k;
            if (map.find(tmp) != map.end()) {
                res += map[tmp];
            }
            ++map[tmp];
        }
        return res;
    }
```
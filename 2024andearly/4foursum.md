# 4. Four Sum
> [Problem link][1]  
>Given an array nums of n integers, return an array of all the >unique quadruplets [nums[a], nums[b], nums[c], nums[d]] such that:
>0 <= a, b, c, d < n
>a, b, c, and d are distinct.
>nums[a] + nums[b] + nums[c] + nums[d] == target
>You may return the answer in any order.

- 思路同三数之和一样,考虑两层循环,用双指针找出另外两个数.
- 复杂度为$O(n^3)$.

```C++
vector<vector<int>> FourSum(vector<int>& nums, int target)
{
    vector<vecto<int>> ret;
    sort(nums.begin(), nums.end());
    for (int i = 0; i < nums.size(); i++)
    {
        if (i > 0 && nums[i] == nums[i - 1]) continue; // 去重
        for (int j = i + 1; j < nums.size(); j++)
        {
            if (j > i + 1 && nums[j] == nums[j - 1]) continue; // 去重
            int left = j + 1, right = nums.size() - 1;
            while (left < right)
            {
                long sum = long(nums[i]) + nums[j] + nums[left] + nums[right]; // 避免溢出
                if (sum > target) right--;
                else if (sum < target) left++;
                else
                {
                    ret.push_back({nums[i], nums[j], nums[left], nums[right]});
                    while (left < right && nums[left] == nums[left + 1]) left++; // 去重
                    while (left < right && nums[right] == nums[right - 1]) right--;
                    left++;
                    right--;
                }
            }
        }
        return ret;
    }
}
```

[1]: https://leetcode.com/problems/4sum/
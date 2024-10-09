# 15. 3Sum

> [Problem link][ 1 ]

>Given an integer array nums, return all the triplets [nums[i], nums[j], nums[k]] such that i != j, i != k, and j != k, and nums[i] + nums[j] + nums[k] == 0.***Notice that the solution set must not contain duplicate triplets***.


- 首先,对数组进行排序.用$i$遍历数组,对其右边剩余元素数组,使用双指针$left$和$right$分别指向$i + 1$和$nums.size() - 1$的位置.
- 然后我们比较$nums[i] + nums[left] + nume[right]$与$0$的大小,如果大于$0$,则$right$左移,反之,则$left$右移.而当两者相等时,我们将其加入结果数组中并同时将$left$右移,将$right$左移.PS:在同时移动时,需要判断下个元素与左右指针的大小关系,如果相等,则跳过.
- 当$i$遍历到数组中间时,需要判断其与前一个元素是否相等,如此则跳过.
- 最后返回结果数组.

```C++
vector<vector<int>> threeSum(vector<int>& nums)
{
    vector<vector<int>> ret;
    sort(nums.begin(), nums.end());
    for (int i = 0; i < nums.size(); i++)
    {
        if (i > 0 && nums[i] == nums[i - 1]) continue;
        int left = i + 1, right = nums.size() - 1;
        while (left < right)
        {
            int sum = nums[i] + nums[left] + nums[right];
            if (sum > 0) right--;
            else if (sum < 0) left++;
            else
            {
                ret.push_back({nums[i], nums[left], nums[right]});
                while (left < right && nums[left] == nums[left + 1]) left++;
                while (left < right && nums[right] == nums[right - 1]) right--;
                left++;
                right--;
            }
        }
    }
    return ret;
}
```

[1]: https://leetcode.com/problems/3sum/
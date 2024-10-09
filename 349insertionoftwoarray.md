# 349. Intersection of Two Arrays

> Given two intergers arrays ***nums1 and nums2***, return their 
> intersection.Each element in the result must appear ***only once*** and you may return the result in any order.


- 初始化一个unordered_set和unordered_map,map用来记录num1中出现的元素,遍历num2,如果nums2[i]在map中存在,则将其加入set中,最后用set初始化一个新的vector返回即可.

```C++
std::vector<int> intersection(std::vector<int>& nums1, std::vector<int>& nums2)
{
    std::unordered_set<int> set;
    std::unordered_map<int, bool> map;
    for (int num : nums1) map[num] = true;
    for (int num : nums2)
    {
        if (map[num] == true) set.insert(num);
    }
    return std::vector<int> (set.begin(), set.end());
}

```
# 350. Intersection of Two Arrays II

> Given tow integers arrays ***nums1 and nums2***, return their 
> intersection.Each element in the result must appear ***as many times
> as it show in both arrays*** and you may return the result in any order.

- 初始化一个unordered_map,map用来记录两个数组中长数组的的元素及其出现次数,遍历短数组,如果短数组元素在map中存在且键值大于$0$,则将其加入到结果数组中,并将键值减$1$.

```C++
std::vector<int> intersection(std::vector<int>& nums1, std::vector<int>& nums2)
{
    std::unordered_map<int, int> map;
    std::vector<int> ret;
    if (nums1.size() < nums2.size()) std::swap(nums1, nums2);
    for (int num : nums1) map[num]++
    for (int num : nums2)
    {
        if (map.find(num) != map.end() && map[num] > 0) ret.push_back(num);
    }
    return ret;
}

```

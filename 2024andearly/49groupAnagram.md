# 49. Group Anagrams

> Given an array of strings, group anagrams together.  

- 初始化一个unordered_map, key为字符串排序后的结果, value为一个
vector<string>用来存放互为字母异位词的字符串.
- 遍历字符串数组,对每个字符串进行排序,判断其是否在unordered_map中,如果
存在,将其插入到数组中;如果不存在,则初始化一个pair,其将排序后的字符串作为key,将原字符串作为一个数组中的元素,把这个pair插入到unordered_map中.
- 初始化一个ret ***(字符数组的数组)***,把unordered_map中的所有key的value值拷贝到ret中,并返回ret.

```C++
std::vector<vector<string>> groupAnagrams(std::vector<string>& strs)
{
    std::vector<vector<string>> ret;
    std::unordered_map<string, vector<stinrg>> map;
    for (std::sting& s : strs)
    {
        std::string temp = s;
        std::sort(temp.begin(), temp.end());
        if (map.count(temp)) map[temp].push_back(s);
        else map.insert(std::pair<string, vector<string>>(temp, {s})); 
    }
    for (std::pair<string, vector<string>>& p : map) ret.push_back(p.second);
    return ret;
}
## 242. Valid Anagram  

Given two strings s and t, write a function to determine if t is an anagram of s.

- 初始化一个长度为26的数组,用于记录每个元素出现的次数.
- 遍历字符串s,对于其中元素使数组值加一;遍历t,对于其中元素使数组值减一,
并检查值是否小于$0$,如果是,则直接返回***false***.
- 上述过程结束后返回***true***.

```C++
bool isAnagram(sting s, string t)
{
    vector<int> count(26, 0);
    for (char c : s) count[c - 'a']++;
    for (char c : t)
    {
        if (--count[c - 'a'] < 0) return false;
    }
    return true;
}
```

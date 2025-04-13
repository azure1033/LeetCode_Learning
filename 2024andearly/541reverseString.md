# 541. Reverse String II

> Given a string s and an integer k, reverse the first k characters for every 2k characters counting from the start of the string.
If there are fewer than k characters left, reverse all of them. If there are less than 2k but greater than or equal to k characters, then reverse the first k characters and leave the other as original.

- 思路很简单,考虑末尾的情况,如果多余的字符串小于等于$k$,全部反转即可;如果多余字符串大于$k$,只反转前$k$个字符即可.

```C++
void reverse(string& s, int first, int end)
{
    int left = first;
    int righrt = end - 1;
    while (left < right)
    {
        int temp = s[left];
        s[left] = s[right];
        s[right] = temp;
        left++;
        right--;
    }
}

string reverseStr(string s, int k)
{
    int n = s.size() / (2 * k);
    int leave = s.size() %  (2 * k);
    int count = 0;
    while (count < n)
    {
        reverse(s, count * 2 * k, count * 2 * k + k - 1);
        count++;
    }
    if (leave && leave <= k) reverse(s, count * 2 * k, s.size() - 1);
    else reverse(s, count * 2 * k, count * 2 * k + k - 1);
    return s;
}

```
```C++ 
使用库函数
string reverseStr(string s, int k)
{
    for (int i = 0; i < s.size(); i+= 2 * k)
    {
        if (i + k <= s.size()) reverse(s.begin() + i, s.begin() + i + k);
        else reverse(s.begin() + i, s.end());
    }
    return s;
}
```
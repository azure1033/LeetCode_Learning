# 151. Reverse Words in a String

> Given an input string s, reverse the order of the words.  
A word is defined as a sequence of non-space characters. The words in s will be separated by at least one space.  
Return a string of the words in reverse order concatenated by a single space.  
> Note that s may contain leading or trailing spaces or multiple spaces between two words. The returned string should only have a single space separating the words. Do not include any extra spaces.


- 初始化一个字符串,用以输出.
- 先去除字符串前端的空格,避免其影响输出.
- 用两个指针同时指向字符串末尾,一个遇到空格就跳过,一个遇到空格就停止.
- 这两个指针可以标识字符串中的单词, 将其加入结果字符串中.
  
``` C++
string reverseWords(string s)
{
    string ret;
    int index = 0;
    while (s[index] == ' ') index++;
    int fast = s.size() - 1;
    int slow = s.size() - 1;
    while (slow >= index && fast >= index)
    {
        if (fast != s.size() - 1) ret += ' ';
        while (slow >= index && s[slow] == ' ') slow--;
        fast = slow;
        while (fast >= index && s[fast] != ' ') fast--;
        ret += s.substr(fast + 1, slow - fast);
        slow = fast;
    }
    return ret;
}

```

``` C++
考虑先去除多余空格,再整体反转字符串,最后调整单词顺序.
void removeextraspaces(string& s)
{
    int slow = 0;
    for (int i = 0; i < s.size(); ++i)
    {
        if (s[i] != ' ')
        {
            if (slow != 0) s[slow++] = ' ';
            while (i < s.size() && s[i] != ' ') s[slow++] = s[i++];
        }
    }
    s.resize(slow);
}

string reverseWords(string s)
{
    removeextraspaces(s);
    reverse(s.begin(), s.end());
    int start = 0;
    for (int i = 0; i <= s.size(); ++i)
    {
        if (i == s.size() || s[i] == ' ') 
        {
            reverse(s.begin() + start, s.begin() + i);
            start = i + 1;
        }
    }
    return s;
}
```
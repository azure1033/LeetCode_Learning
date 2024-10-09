# 202. Happy Number

Write an algorithm to determine if a number is "happy". A happy
number is a number defined by the following process: Starting with
any positive integer, replace the number by the sum of the squares
of its digits, and repeat the process until the number equals 1
(where it will stay) or ***it loops endlessly in a cycle*** which does not include 1.
Those numbers for which this process ends in 1 are happy numbers.


- 由于有可能陷入无限循环,所以必须记录每次循环的结果,如果出现重复的结果,
则说明该数不是Happy Number.
- 具体实现上的话, 使用unordered_set来记录每次循环的结果,如果出现重复的结果,就直接返回false.

```C++
bool getsum(int n)
{
    int sum = 0;
    while (n)
    {
        sum += (n % 10) * (n % 10);
        n /= 10;
    }
    return sum;
}

bool isHappy(int n)
{
    unordered_set<int> set;
    while (1)
    {
        int sum = getsum(n);
        if (sum == 1) return true;
        if (set.find(sum) != set.end()) return false;
        set.insert(sum);
        n = sum;
    }
}

```
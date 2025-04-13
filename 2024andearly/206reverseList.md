# Reverse a list in C++ LeettCode 206
## Problem statemenet
> Given the head of a singly LinkedList, reverse the LinkedList.  
>  return the new head of the reversed LinkedList.   

### 双指针法
1. 初始化一个pre指针,指向nulltr的;一个cur指针,指向头节点.
2. 进入循环,当cur指针不为nullptr时,执行以下操作:
    - 初始化一个temp指针, 指向cur的下一个节点**因为接下来我们要改变cur->next,即指反转**.
    - 将cur->next指向pre,即完成反转.
    - 将pre指向cur,cur指向temp,完成移动.
3. 完成循环后,pre指针指向原链表的最后一个节点,就是反转后的头节点.因此,返回pre即可.

```C++
ListNode* reverseList(ListNode* head)
{
    ListNode* pre = nullptr;
    ListNode* cur = head;
    while (cur)
    {
        ListNode* temp = cur->next;
        cur->next = pre;
        pre = cur;
        cur = temp;
    }
    return pre;
}

struct ListNode {
    int val;
    ListNde* next;
    ListNode(int val) : val(val), next(nullptr) {}
};
```


### 递归法
1. 递归的基准情况是cur为nullptr,则返回prev.
2. 递归的操作是:
    - 初始化一个temp指针,指向cur->next.
    - 将cur->next指向prev,即完成反转.
    - 返回reverse(cur, temp).
```C++
ListNode* reverse(ListNode* prev, ListNode* cur)
{
    if (!cur) return prev;
    ListNode* temp = cur->next;
    cur->next = prev;
    return reverse(cur, temp);
}

ListNode* reverseList(ListNode* head)
{
    return reverse(nullptr, head);
}
```
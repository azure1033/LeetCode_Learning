# 142. Linked List Cycle II

## Problem
> Given a linked list, return the node where the cycle begins. If there is no cycle, return null.

To represent a cycle in the given linked list, we use an integer pos which represents the position (0-indexed) in the linked list where the tail connects to. If pos is -1, then there is no cycle in the linked list.

### Solution
1. 初始化两个指针, **slow** 和**fast**, **slow**指针每次走一步,**fast**指针每次走两步.
2. 若链表中存在环,则**slow**指针和**fast**指针必定会在环内相遇,因为两者每次移动的距离之差为一个节点.
3. 设头节点到环形入口的节点数 **(节点数计算左开右闭)** 为 $x$, 环形入口到相遇节点的节点数为 $y$, 相遇节点到绕一圈回到入口的节点数为 $z$.
4. 计算到相遇时slow指针经过 $x + y$ 个节点, fast指针经过 $x + y + n(y + z)$ 个节点(其中$n$为绕环的圈数,其值必然不小于$1$),显然有, $2(x + y) = x + y + n(y + z)$ .
> 稍微计算下, 可以得到 $x = (n - 1)(y + z) + z$.  
 - 那么想要找到环形入口可以初始化两个指针,一个指向**head**, 一个指向快慢指针的相遇节点,命名为***index1***和***index2***,可以知道,当两者相遇时,就是环形入口.

```C++
ListNode* detectcycle(ListNode* head)
{
    ListNode* fast = head;
    ListNode* slow = head;
    while (fast && fast->next)
    {
        fast = fast->next->next;
        slow = slow->next;
        if (fast == slow)
        {
            ListNode* index1 = head;
            ListNode* index2 = fast;
            while (index1 != index2)
            {
                index1 = index1->next;
                index2 = index2->next;
            }
            return index1;
        }
    }
    return nullptr;
}
```
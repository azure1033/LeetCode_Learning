# removeNthFromEnd LeetCode 19

## problem  
> Given a head of a linked list, remove the nth node from the end
> of the list and return its head.

1. 初始化两个指针, 均指向dummyNode
2. fast指针先走 n + 1步, 而后fast和slow指针一起遍历至链表末尾,
当fast到达末尾时, slow指向倒数第 n - 1个节点, 即待删除节点的前驱节点.
3. 删除节点,返回dummyNode->next.

``` C++
ListNode* removeNthFromEnd(ListNode* head, int n)
{
    ListNode* dummyNode = new ListNode(0);
    dummyNode->next = head;
    ListNode* fast = dummyNode;
    ListNode* slow = dummyNode;
    for (int i = 0; i < n + 1; i++) fast = fast->next;
    while (fast)
    {
        fast = fast->next;
        slow = slow->next;
    }
    return slow->next;
}

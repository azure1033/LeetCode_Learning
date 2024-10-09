# Swap Pairs LeetCode 24
> Given a Linked List, swap every two adjacent nodes and return its
> head.**(only nodes themselves may be changed).**

1. 初始化一个虚拟指针,指向头节点.
2. 用一个指针"cur"遍历链表,每次移动两个节点,并交换它们的指针.**实现细节看代码注释**.
3. 最后返回虚拟指针的下一个节点.

``` C++
ListNode* swapPairs(ListNode* head)
{
    ListNode* dummyNode = new ListNode(0);
    dummyNode->next = head;
    ListNode* cur = dummyNode;
    while (cur->next && cur->next->next)
    {
        // 总共会涉及三个节点, cur, temp1, temp3
        // temp1是cur的下一个节点, temp3是下次交换的第一个节点
        // 交换后temp1->next指向temp3, 将cur指向temp1
        ListNode* temp1 = cur->next;
        ListNode* temp3 = temp1->next->next;
        
        cur->next = temp1->next; // 
        cur->next->next = temp1;
        temp1->next = temp3;

        cur = temp1; // 移动到要交换的两节点的前一个节点
    }
    return dummyNode->next;
}
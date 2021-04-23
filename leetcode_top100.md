# 一. [两数之和](https://leetcode-cn.com/problems/two-sum/)
  - 1. 暴力穷举（**时间复杂度较高**）
  - 2. **哈希表方式搜索（利用字典）**
  - ***python中的字典***
###
# 二. [两数相加](https://leetcode-cn.com/problems/add-two-numbers/submissions/)
  - 1. 首先将两个链表表示数值分别转化为两个int变量，相加后，将结果再转化为链表
```
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def addTwoNumbers(self, l1: ListNode, l2: ListNode) -> ListNode:
        value1, value2 = 0, 0;
        i = 0
        while l1.next != None:
            value1 = value1 + l1.val * 10 ** i
            i = i + 1
            l1 = l1.next
        value1 = value1 + l1.val * 10 ** i

        i = 0
        while l2.next != None:
            value2 = value2 + l2.val * 10 ** i
            i = i + 1
            l2 = l2.next
        value2 = value2 + l2.val * 10 ** i

        value = value1 + value2
        
        i = 0
        firstnode = ListNode(0)
        while value > 0:
            number = value % 10
            tempNode = ListNode(number)
            if i > 0:
                temppoint.next = tempNode
            else:
                firstnode = tempNode
            temppoint = tempNode

            i = i + 1
            value = value // 10
        
        return firstnode
```
  - 2. 注意python中没有问号表达式，采用`x if a else y`来实现; python中`int()`是向0取整，`\\`是向下取整
  - ***python中的链表数据结构***<https://zhuanlan.zhihu.com/p/60057180>
  - 对于链表长短不一的情况，考虑到后边为None是设置为0，即`[7, 8]`看作`[7, 8, 0]`

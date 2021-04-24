# 一. [两数之和](https://leetcode-cn.com/problems/two-sum/)
  - 1. 暴力穷举（**时间复杂度较高**）
  - 2. **哈希表方式搜索（利用字典）**
  - ***python中的字典***
###
# 二. [两数相加](https://leetcode-cn.com/problems/add-two-numbers/submissions/)
  - 1. 第一次做：首先将两个链表表示数值分别转化为两个int变量，相加后，将结果再转化为链表
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
  - 题解：对于链表长短不一的情况，考虑到后边为None是设置为0，即`[7, 8]`看作`[7, 8, 0]`，然后对两个链表进行遍历，设置进位标记。
# 三、[整数反转](https://leetcode-cn.com/problems/reverse-integer/)
  - 方法1： 数字转为字符串，反转后再转回数字
  - 方法2： 从低位到高位遍历数字，每次弹出一个数值并放入要返回的数值。**注意判断返回的数值是否溢出！**
  - 注意的问题：
    - python中`int`和`//`，一个是向0取整，一个是向下取整
# 四、[回文数](https://leetcode-cn.com/problems/palindrome-number/)
  - 该问题与**整数反转**有些类似，可以转为字符串处理、也可以先反转完整的数字再处理
  - 题解： 考虑反转一般的数字就能够判断，主要的问题是判断什么时候达到一半，此时需要分为偶数位数和奇数位数分别判断。若偶，则数值相等；若奇，则反转数值变量大于原数值变量；
# 五、[罗马数字转整数](https://leetcode-cn.com/problems/roman-to-integer/submissions/)
  - 方法1：（第一次做）：
```
class Solution:
    def romanToInt(self, s: str) -> int:
        num = 0
        d_s2n = {"I": 1, "V": 5, "X": 10, "L": 50, 
                 "C": 100, "D": 500, "M": 1000, }
        for idx, st in enumerate(s):
            if st == "V" or st == "L" or st == "D" or st == "M" or idx == len(s) - 1:
                num = num + d_s2n[st]
            elif st == "I":
                if s[idx + 1] == "V" or  s[idx + 1] == "X":
                    num = num - 1
                else:
                    num = num + 1
            elif st == "X":
                if s[idx + 1] == "L" or  s[idx + 1] == "C":
                    num = num - 10
                else:
                    num = num + 10
            elif st == "C":
                if s[idx + 1] == "D" or  s[idx + 1] == "M":
                    num = num - 100
                else:
                    num = num + 100
        return num
```
  - 方法2（题解）：考虑当当前字符的数值小于右边时，实际是减上当前字符
```
class Solution:
    def romanToInt(self, s: str) -> int:
        num = 0
        d_s2n = {"I": 1, "V": 5, "X": 10, "L": 50, 
                 "C": 100, "D": 500, "M": 1000, }
        for idx in range(len(s) - 1):
            if d_s2n[s[idx]] < d_s2n[s[idx + 1]]:
                num -= d_s2n[s[idx]]
            else:
                num += d_s2n[s[idx]]
        num += d_s2n[s[len(s) - 1]]

        return num         
```

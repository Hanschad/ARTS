# AddTwoNumbers
## 题目
You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

Example:

Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 0 -> 8
Explanation: 342 + 465 = 807.

## 解答
```java
public ListNode addTwoNumbers(ListNode l1, ListNode l2){
    ListNode result = new ListNode(0);
    ListNode pres = result;
    ListNode p1 = l1;
    ListNode p2 = l2;
    int carry = 0;

    while (p1 !=null || p2!=null){
        int sum = carry;
        if (p1 != null){
            sum += p1.val;
            p1 = p1.next;
        }
        if (p2 != null){
            sum += p2.val;
            p2 = p2.next;
        }

        carry = sum/10;
        int val = sum % 10;
        pres.next = new ListNode(val);
        pres = pres.next;
    }
    if (carry > 0){
        pres.next = new ListNode(carry);
    }
    return result.next;
}
```
## 解题思路
这道题的题意是在模拟加法运算。所以解题总思路为遍历两个链表，对两个链表结点的值求和，保留进位，填充和的个位到结果链表中。需要注意链表结束后，如果有进位大于0也要加到链表中。

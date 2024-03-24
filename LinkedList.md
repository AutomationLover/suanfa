# name


## when using


## template
用dummy 指向head 可以省去 判断head是否为空

## examples
```python

class Solution:
    def addTwoNumbers(self, l1: Optional[ListNode], l2: Optional[ListNode]) -> Optional[ListNode]:
        dummy = ListNode() #assign a dummy node
        curr = dummy # current pointer pointing at dummy node
        carry = 0

        while l1 or l2 or carry:
            v1 = l1.val if l1 else 0
            v2 = l2.val if l2 else 0
            val = v1+v2+carry
            carry = val//10
            val = val%10

            # new digit
            curr.next = ListNode(val)
            curr = curr.next
            l1 = l1.next if l1 else None
            l2 = l2.next if l2 else None

        return dummy.next


```

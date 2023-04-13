#CST101-13-04-2023 
#13-04-2023


Given the `head` of a singly linked list, reverse the list, and return _the reversed list_.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/02/19/rev1ex1.jpg)

**Input:** head = `[1,2,3,4,5]`
**Output:** `[5,4,3,2,1]`

**Example 2:**

![](https://assets.leetcode.com/uploads/2021/02/19/rev1ex2.jpg)

**Input:** head = `[1,2]`
**Output:** `[2,1]`

**Example 3:**

**Input:** head = `[]`
**Output:** `[]`

**Constraints:**

-   The number of nodes in the list is the range `[0, 5000]`.
-   `-5000 <= Node.val <= 5000`

**Follow up:** A linked list can be reversed either iteratively or recursively. Could you implement both?



```cpp
class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        if(!head or !head->next)
            return head;
        ListNode* prev = NULL, *cur = head, *fast = head->next;
        while(fast){
            cur->next = prev;
            prev = cur;
            cur = fast;
            fast = fast->next;
        }
        cur->next = prev;
        return cur;
    }
};
```


```cpp
class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        if(!head or !head->next)
            return head;
        ListNode* reversed = reverseList(head->next);
        head->next->next = head;
        head->next = NULL;
        return reversed;
    }
};
```
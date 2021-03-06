# Linked Lists

+ [Reorder List](#reorder-list)
+ [Linked List Cycle II](#linked-list-cycle-2)
+ [Linked List Cycle](#linked-list-cycle)
+ [Merge Two Sorted Lists](#merge-two-sorted-lists)
+ [Remove Nth Node From End of List](#remove-nth-node-from-end-of-list)
+ [Middle of the Linked List](#middle-of-the-linked-list)
+ [Delete Node in a Linked List](#delete-node-in-a-linked-list)
+ [Palindrome Linked List](#palindrome-linked-list)
+ [Reverse Linked List](#reverse-linked-list)
+ [Remove Linked List Elements](#remove-linked-list-elements)
+ [Intersection of Two Linked Lists](#intersection-of-two-linked-lists)
+ [Sort List](#sort-list)

## Reorder List

https://leetcode.com/problems/reorder-list/

```cpp
class Solution {
 public:
  ListNode* middleNode(ListNode* head) {
    ListNode* middle = head;
    while (head->next) {
      middle = middle->next;
      head = head->next;
      if (head->next) head = head->next;
    }
    return middle;
  }
  ListNode* reverseList(ListNode* head) {
    ListNode* current = head;
    ListNode* prev = NULL;
    while (current) {
      ListNode* next = current->next;
      current->next = prev;
      prev = current;
      current = next;
    }
    return prev;
  }
  void reorderList(ListNode* head) {
    if (!head || !head->next) return;
    ListNode* rev = reverseList(middleNode(head));
    ListNode* temp;
    while (head->next) {
      temp = head->next;
      head->next = rev;
      if (rev) rev = rev->next;
      head = head->next;
      if (head) head->next = temp;
      head = temp;
    }
  }
};
```
## Linked List Cycle II

https://leetcode.com/problems/linked-list-cycle-ii/submissions/

```cpp
class Solution {
 public:
  ListNode* detectCycle(ListNode* head) {
    if (!head) return NULL;
    ListNode* slow = head;
    ListNode* fast = head;
    while (fast) {
      slow = slow->next;
      fast = fast->next;
      if (fast) fast = fast->next;
      if (fast == slow) break;
    }
    if (!fast) {
      return NULL;
    }
    fast = head;
    while (fast != slow) {
      fast = fast->next;
      slow = slow->next;
    }
    return fast;
  }
};
```
## Linked List Cycle

https://leetcode.com/problems/linked-list-cycle/submissions/

```cpp
class Solution {
 public:
  bool hasCycle(ListNode* head) {
    if (!head) return NULL;
    ListNode* slow = head;
    ListNode* fast = head;
    while (fast) {
      slow = slow->next;
      fast = fast->next;
      if (fast) fast = fast->next;
      if (fast == slow) break;
    }
    return fast != NULL;
  }
};
```
## Merge Two Sorted Lists

https://leetcode.com/problems/merge-two-sorted-lists/

```C++
class Solution {
 public:
  ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
    if (!l1) return l2;
    if (!l2) return l1;
    ListNode* current = l1->val > l2->val ? l2 : l1;
    if (current == l1)
      l1 = l1->next;
    else
      l2 = l2->next;
    ListNode* newList = current;
    while (l1 && l2) {
      current->next = l1->val > l2->val ? l2 : l1;
      if (current->next == l1)
        l1 = l1->next;
      else
        l2 = l2->next;
      current = current->next;
    }
    current->next = l1 ? l1 : l2;
    return newList;
  }
};
```
## Remove Nth Node From End of List

https://leetcode.com/problems/remove-nth-node-from-end-of-list/

```cpp
class Solution {
 public:
  ListNode* removeNthFromEnd(ListNode* head, int n) {
    ListNode* cur = head;
    ListNode* N_elem = head;
    while (n != 0) {
      n--;
      cur = cur->next;
    }
    N_elem = cur;
    if (!N_elem) return head->next;
    cur = head;
    while (N_elem->next) {
      cur = cur->next;
      N_elem = N_elem->next;
    }
    cur->next = cur->next->next;
    return head;
  }
};
```

## Middle of the Linked List

https://leetcode.com/problems/middle-of-the-linked-list/

```cpp
class Solution {
 public:
  ListNode* middleNode(ListNode* head) {
    ListNode* middle = head;
    while (head->next) {
      middle = middle->next;
      head = head->next;
      if (head->next) head = head->next;
    }
    return middle;
  }
};
```

## Delete Node in a Linked List

https://leetcode.com/problems/delete-node-in-a-linked-list/

```cpp
class Solution {
 public:
  void deleteNode(ListNode* node) {
    ListNode* temp = node->next;
    node->val = temp->val;
    node->next = temp->next;
    delete (temp);
  }
};
```

## Palindrome Linked List

https://leetcode.com/problems/palindrome-linked-list/

```cpp
class Solution {
 public:
  ListNode* middleNode(ListNode* head) {
    ListNode* middle = head;
    while (head->next) {
      middle = middle->next;
      head = head->next;
      if (head->next) head = head->next;
    }
    return middle;
  }
  ListNode* reverseList(ListNode* head) {
    ListNode* current = head;
    ListNode* prev = NULL;
    while (current) {
      ListNode* next = current->next;
      current->next = prev;
      prev = current;
      current = next;
    }
    return prev;
  }
  bool isPalindrome(ListNode* head) {
    if (!head || !head->next) return true;
    ListNode* mid = middleNode(head);
    ListNode* rev = reverseList(mid);
    while (head != mid) {
      if (head->val != rev->val) return false;
      head = head->next;
      rev = rev->next;
    }
    return true;
  }
};
```
##  Reverse Linked List

https://leetcode.com/problems/reverse-linked-list/

```cpp
class Solution {
 public:
  ListNode* reverseList(ListNode* head) {
    ListNode* current = head;
    ListNode* prev = NULL;
    while (current) {
      ListNode* next = current->next;
      current->next = prev;
      prev = current;
      current = next;
    }
    return prev;
  }
};
```
## Remove Linked List Elements

https://leetcode.com/problems/remove-linked-list-elements/

```cpp
class Solution {
 public:
  ListNode* removeElements(ListNode* head, int val) {
    ListNode* current = head;
    ListNode* prev = NULL;
    while (current && current->val == val) {
      head = current->next;
      delete (current);
      current = head;
    }
    while (current) {
      if (current->val == val) {
        prev->next = current->next;
        delete (current);
        current = prev->next;
        continue;
      }
      prev = current;
      current = current->next;
    }
    return head;
  }
};
```
## Intersection of Two Linked Lists

https://leetcode.com/problems/intersection-of-two-linked-lists/

```cpp
class Solution {
 public:
  ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
    ListNode *curA = headA;
    ListNode *curB = headB;
    while (curA != curB) {
      if (!curA)
        curA = headB;
      else
        curA = curA->next;
      if (!curB)
        curB = headA;
      else
        curB = curB->next;
    }
    return curA;
  }
};
```
## Sort List

https://leetcode.com/problems/sort-list/

```cpp
class Solution {
 public:
  ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
    if (!l1) return l2;
    if (!l2) return l1;
    ListNode* current = l1->val > l2->val ? l2 : l1;
    if (current == l1)
      l1 = l1->next;
    else
      l2 = l2->next;
    ListNode* newList = current;
    while (l1 && l2) {
      current->next = l1->val > l2->val ? l2 : l1;
      if (current->next == l1)
        l1 = l1->next;
      else
        l2 = l2->next;
      current = current->next;
    }
    current->next = l1 ? l1 : l2;
    return newList;
  }
  ListNode* middleNode(ListNode* head) {
    ListNode* middle = head;
    ListNode* prev;
    while (head->next) {
      prev = middle;
      middle = middle->next;
      head = head->next;
      if (head->next) head = head->next;
    }
    prev->next = NULL;
    return middle;
  }
  ListNode* sortList(ListNode* head) {
    if (!head || !head->next) return head;
    return mergeTwoLists(sortList(head), sortList(middleNode(head)));
  }
};
```

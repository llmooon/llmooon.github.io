---
layout: post
comments: true
categories: Algorithm
tag : 알고리즘_구현
---

## LeetCode - AddTwoSum

- 단순한 연결리스트 구현

```c++
class Solution {
public:
    ListNode* trace(ListNode*l1, ListNode* l2, int over){
        if(!l1 && !l2 && over==0) return NULL;
        int num1=0,num2=0;
        
        if(l1!=NULL) num1 = l1->val;
        if(l2!=NULL) num2 = l2->val;
        int sum = num1 + num2 + over;
        
        ListNode *now = new ListNode(sum%10);
        
        if(l1 && l2){
            ListNode *node =  trace(l1->next, l2->next, sum/10);
            now->next = node;
        }
        else if(l1){
            ListNode *node =  trace(l1->next, NULL, sum/10);
            now->next = node;
        }
        else if(l2){
            ListNode *node =  trace(NULL, l2->next, sum/10);
            now->next = node;
        }
        
        return now;
    }
    
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        return trace(l1,l2,0);
    }
};



```
---
layout: post
comments: true
categories: Algorithm
tag : 알고리즘
---

## LeetCode - Valid Parentheses

- 오랜만에 문제를 풀어보았다! 끙,,, ! 이 문제는 대학생때 수업 들으면서 많이 들어서 풀이는 쉽게 생각났다. 하지만 오랜만의 코딩이라 그런지 사소한 오류가 많이 나서 많이 틀렸다ㅠㅠ
- 문제를 풀기전에 어떻게 코딩할지 생각하고 코딩해야겠다.

###### 보완할 수 있는 점

- 지금 코딩 같은 경우는 조금 노가다 같고 코드 길이 김. 괄호의 종류가 더 많아지면 더더더 귀찮음! -> Map 자료구조를 이용하면 조금 더 노가다를 줄일 수 있다.

```c++
class Solution {
public:
    
    bool isValid(string s) {

        stack<char> bucket;
        int len = s.size();
        bool ans=true;
        
        for(int i=0;i<len && ans ;i++){
            if(s[i]=='(' || s[i]== '[' || s[i]=='{'){
                bucket.push(s[i]);
            }
            else if(bucket.empty())
                ans=false;
            else if(s[i]==')'){
                if(bucket.top()!='(') ans=false;
                bucket.pop();
            }
            else if(s[i]=='}'){
                if(bucket.top()!='{') ans=false;
                bucket.pop();
            }
            else if(s[i]==']'){
                if(bucket.top()!='[') ans=false;
                bucket.pop();
            }
        }
        
        if(bucket.empty()==false) ans=false;
        return ans;
    }
};
```
---
layout: post
comments: true
categories: Algorithm
tag : 알고리즘
---

## LeetCode - Roman to Integer

###### 보완할 수 있는 점

- 빼기 연산을 해야하는 문자열이 겹칠 경우가 없다는 것을 잘 생각하면 그냥 문자열에 포함 되어있나 안되어있나로도 찾을 수 있다.
- map 자료 구조를 구지 안써도 된다는점.

```c++
class Solution {
public:
    int romanToInt(string s) {
        
        map<char,int> m;
        m['I']=1, m['V']=5, m['X']=10, m['L']=50, m['C']=100, m['D']=500, m['M']=1000;
        int len = s.size();
        int ans = 0;
        
        for(int i=0;i<len;i++){
            if(i==len-1){
                ans+=m[s[i]];
                continue;
            }
            if(s[i]=='I' && s[i+1] =='V') {
                ans+=m[s[i+1]]-m[s[i]];
                i++;
            }
            else if(s[i]=='I' && s[i+1] =='X') ans+=m[s[i+1]]-m[s[i++]];
            else if(s[i]=='X' && s[i+1] =='L') ans+=m[s[i+1]]-m[s[i++]];
            else if(s[i]=='X' && s[i+1] =='C') ans+=m[s[i+1]]-m[s[i++]];
            else if(s[i]=='C' && s[i+1] =='M') ans+=m[s[i+1]]-m[s[i++]];
            else if(s[i]=='C' && s[i+1] =='D') ans+=m[s[i+1]]-m[s[i++]];
            else ans+=m[s[i]];
            
        }
        return ans;
    }
};
```
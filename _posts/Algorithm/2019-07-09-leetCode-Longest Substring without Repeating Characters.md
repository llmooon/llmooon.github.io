---
layout: post
comments: true
categories: Algorithm
tag : 알고리즘
---

## LeetCode - ThreeSum

- two pointer를 이용하여 중복되지 않은 수열의 길이를 구한다.

```c++
class Solution {
    int arr[1000];
public:
    int lengthOfLongestSubstring(string s) {
        int left=0,max_cnt=0,len=s.size();
        for(int i=0;i<len;i++){
            int idx=s[i]-0;
            if(arr[idx]!=0){
                while(left<i && (s[i]!=s[left])){
                    arr[s[left]-0]--;
                    left++;
                }
                arr[s[left]-0]--;
                left++;
            }
            arr[idx]++;
            max_cnt = max(max_cnt, i-left+1);
        }
        return max_cnt;
    }
};

```
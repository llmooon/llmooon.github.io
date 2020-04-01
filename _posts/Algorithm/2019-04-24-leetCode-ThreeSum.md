---
layout: post
comments: true
categories: Algorithm
tag : 알고리즘
---

## LeetCode - ThreeSum

- 쓰리포인터를 이용하여 문제 해결.
- 쓰리포인터  처음 써봐서 신기했다. 
- 중복된 숫자 처리를 while문을 이용하여 그냥 넘어가게 한다면 시간을 더 줄일 수 있을 거 같다.

```c++
class Solution {
public:
    vector<vector<int>> threeSum(vector<int>& nums) {
        vector<vector<int> > res;
        set<pair<int,pair<int,int>>> s;
        sort(nums.begin(), nums.end());
        for(int i=0;i<nums.size();i++){
            int left = i+1, right= nums.size()-1;
            while(left<right){
                int sum = nums[i]+nums[left]+nums[right];
                if(sum==0) {
                    //printf("%d %d %d\n",nums[i], nums[left], nums[right]);
                    if(s.find({nums[i],{nums[left],nums[right]}})==s.end()){
                        vector<int> tmp={nums[i], nums[left],nums[right]};
                        s.insert({ nums[i],{nums[left],nums[right]} });

                        res.push_back(tmp);
                    }
                    left++, right--;
                }
                else{
                    if(sum>0) right--;
                    else left++;
                }
                
            }
        }
        return res;
    }
};


```
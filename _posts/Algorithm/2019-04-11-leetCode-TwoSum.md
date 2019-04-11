---
layout: post
comments: true
categories: Algorithm
tag : 알고리즘_해쉬
---

## LeetCode - TwoSum

- 해쉬를 이용하여 나온 값을 저장하며 target-nums[i]의 값이 해쉬에 저장되어 있는가 확인한다.

```c++
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        unordered_map<int,int> indices;
        for(int i=0;i<nums.size();i++){
            if(indices.find(target-nums[i])!=indices.end())
                return {indices[target-nums[i]],i};
            indices[nums[i]]=i;
        }

    return {};
    }
};


```
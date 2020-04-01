---
layout: post
comments: true
categories: Algorithm
tag : 알고리즘
---

- 쉬운 정렬 문제였다.
- 변경이 빈번한 세그먼트 트리

```c++
#include<iostream>
#include<algorithm>
#include<vector>
using namespace std;

int n, num;
vector<int> arr,ans;
int main() {
	scanf("%d", &n);
	for (int i = 0; i < n; i++) {
		scanf("%d", &num);
		arr.push_back(num);
	}
	sort(arr.begin(), arr.end());
	for (int i = n-1; i>=0; i--) {
		if (ans.size() <= arr[i]) {
			ans.push_back(arr[i]);
		}
	}
	cout << ans.size();
}
```
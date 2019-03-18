---
layout: post
comments: true
categories: Algorithm
tag : 알고리즘_그리디
---

-  그리디

```c++
#include<iostream>
#include<algorithm>
#include<vector>
using namespace std;

int n,num,i;
vector<int> input, arr;

int main() {
	scanf("%d", &n);
	for (int i = 0; i < n; i++) {
		scanf("%d", &num);
		input.push_back(num);
	}
	while (i < n) {
		int num = 1;
		while (i < n-1 && input[i] == input[i + 1]) {
			num++;
			i++;
		}
		arr.push_back(num);
		i++;
	}
	int ans = 0;
	for (int i = 0; i < arr.size()-1; i++) {
		ans = max(ans, 2 * min(arr[i], arr[i + 1]));
	}
	printf("%d", ans);
}
```

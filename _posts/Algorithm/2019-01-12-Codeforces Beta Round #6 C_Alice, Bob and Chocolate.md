---
layout: post
comments: true
categories: Algorithm
tag : 알고리즘_투포인터
---

-  양 끝에서 크기가 작은 인덱스를 하나씩 줄여가는 문제

```c++
#include<iostream>
using namespace std;

int n, arr[100010];
int main() {
	scanf("%d", &n);
	for (int i = 0; i < n; i++) {
		scanf("%d", &arr[i]);
	}
	if (n == 1) {
		printf("1 0");
	}
	else {
		int pl = 0, pr = n - 1, l = arr[pl], r = arr[pr];
		while (!(pl + 1 == pr) && pl < n && pr >= 0) {
			if (l <= r) {
				pl++;
				l += arr[pl];
			}
			else {
				pr--;
				r += arr[pr];
			}
		}
		printf("%d %d", pl + 1, n-(pr));
	}
	return 0;
}
```

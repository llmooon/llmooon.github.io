---
layout: post
comments: true
categories: Algorithm
tag : 알고리즘
---



```c++
#include<iostream>
#include<algorithm>
using namespace std;

int a, b;

int main() {
	scanf("%d %d", &a, &b);
	int max_num = max(a, b);
	int right = 6;
	int rest = 6 - max_num + 1;
	for (int i = 6; i >=2; i--) {
		if (rest%i == 0 && right%i==0) {
			rest /= i;
			right /= i;
		}
	}
	printf("%d/%d", rest, right);

}

```

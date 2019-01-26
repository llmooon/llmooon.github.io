---
layout: post
comments: true
categories: Algorithm
tag : 알고리즘_Bfs, 알고리즘_2진수, 알고리즘_완전탐색
---

-  Bfs 풀이,  2진수의 활용, 완전 탐색 등등 다양한 풀이가 존재

```c++
#include<iostream>
#include<algorithm>
#include<vector>
#include<math.h>
using namespace std;
int n;
vector<int> v;


int changeToHex() {
	int nownum = 1,res=0;
	for (int i = 0; i < v.size(); i++) {
		res += (v[i]*nownum);
		nownum *= 10;
	}
	v.clear();
	return res;
}

int getHexPart(int i) {
	while (i) {
		v.push_back(i % 2);
		i /= 2;
	}
	return changeToHex();
}

int main() {
	scanf("%d", &n);
	int i = 0,now=1;
	while (true) {
		i++;
		now = getHexPart(i);
		if (now > n) break;
	}
	printf("%d", i-1);
}
```

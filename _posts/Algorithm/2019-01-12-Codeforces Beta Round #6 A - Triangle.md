---
layout: post
comments: true
categories: Algorithm
tag : 알고리즘_삼각형, 알고리즘_구현
---

-  삼각형의 성질을 잘 알아야 풀 수 있는 문제
   -  삼각형의 가장 긴 변의 길이의 합은 나머지 두 합보다 작아야 한다.

```c++
#include<iostream>
#include<algorithm>
using namespace std;

int arr[4];

void maketri() {
	for (int i = 0; i < 4; i++) {
		for (int j = i + 1; j < 4; j++) {
			for (int k = j + 1; k < 4; k++) {
				int temp[3] = { arr[i],arr[j],arr[k] };
				sort(temp, temp + 3);
				if (temp[0] + temp[1] > temp[2]) {
					printf("TRIANGLE");
					return;
				}
			}
		}
	}
	for (int i = 0; i < 4; i++) {
		for (int j = i + 1; j < 4; j++) {
			for (int k = j + 1; k < 4; k++) {
				int temp[3] = { arr[i],arr[j],arr[k] };
				sort(temp, temp + 3);
				if (temp[0] + temp[1] == temp[2]) {
					printf("SEGMENT");
					return;
				}
			}
		}
	}
	printf("IMPOSSIBLE");
}

int main() {
	for (int i = 0; i < 4; i++) {
		scanf("%d", &arr[i]);
	}
	maketri();
	return 0;
}
```

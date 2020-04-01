---
layout: post
comments: true
categories: Algorithm
tag : 알고리즘
---

## 백준 15764 milking Order

구현 문제이지만 테케가 매우 까다롭다.

```c++

#include<iostream>
#include<stack>
#include<algorithm>
using namespace std;
int n, m, k, before, num, p, idx[110], parent[110], position[110], isin, max_idx,hire[110];
int main() {
	scanf("%d %d %d", &n, &m, &k);
	for (int i = 0; i < m; i++) {
		scanf("%d", &num);
		if (num == 1) isin = 1;
		hire[num] = i+1;
		if (i != 0) parent[num] = before;
		before = num;
	}

	for (int i = 0; i < k; i++) {
		scanf("%d %d", &num, &p);
		position[p - 1] = num;
		idx[num] = p - 1;
		if (isin) {
			if (hire[num] != 0 && hire[num] < hire[1]) max_idx = max(max_idx, p - 1);
		}
	}

	for (int i = 100; i >= 0; i--) {
		if (position[i] != 0) {
			int father = parent[position[i]], now = i - 1;
			if (father != 0 && idx[father] == 0) {
				while (now >= 0 && position[now] != 0) {
					now--;
				}
				position[now] = father;
				if (isin && hire[now]!=0 && hire[now]<hire[1]) max_idx = max(max_idx, now);
			}
		}
	}

	stack<int> v;
	int now = 1;
	while (now != 0 && idx[now] == 0) {
		v.push(now);
		now = parent[now];
	}
	int ans = 0;
	for (; ans <= 100; ans++) {
		if (position[ans] == 1) break;
		if (position[ans] == 0) {
			if (ans < max_idx) continue;
			else {
				int top = 0;
				while (idx[v.top()] != 0)
					top = v.top(), v.pop();
				top = v.top();
				v.pop();
				if (top == 1) break;
			}

		}
	}
	printf("%d", ans + 1);
}
```
---
layout: post
comments: true
categories: Algorithm
tag : 알고리즘_투포인터, 알고리즘_set, 알고리즘_슬라이딩윈도우
---

-  숫자 범위가 k이하 차이나는 범위 중 가장 긴 범위를 구하는 문제.
-  투포인터와 set을 결합하여 문제를 해결하였다.
-  처음에는 투포인터로만 해결이 가능할 거 같았지만 TLE가 났다.
-  자료구조를 잘 활용해야 풀수 있는 문제.

```c++
#include<iostream>
#include<algorithm>
#include<vector>
#include<set>
using namespace std;

int arr[100010],n,k,cnt,diff,ans[100010];

set<pair<int, int> > s;
int max_period, period;
int main() {
	scanf("%d %d", &n, &k);
	for (int i = 0; i < n; i++) {
		scanf("%d", &arr[i]);
	}
	int max_idx = -1;
	for (int r = 0; r < n; r++) {
		s.insert({ arr[r],r });
		auto head = s.begin();
		auto tail = --(s.end());
		while (abs(head->first - tail->first) > k) {
			max_idx = max(max_idx, min(head->second, tail->second));
			if (head->second < tail->second) s.erase(head);
			else s.erase(tail);
			head = s.begin(), tail = --(s.end());
		}
		ans[r] = max_idx + 1;
		//cnt = max(cnt, ans[r]);
		if (diff < r - ans[r]) {
			cnt = 0,diff = r - ans[r];
		}
		if (diff == r - ans[r]) cnt++;
	}
	printf("%d %d\n", diff + 1,cnt);
	for (int i = 0; i < n; i++) {
		if (i - ans[i] == diff) {
			printf("%d %d\n", ans[i] + 1, i + 1);
		}
	}
	return 0;
}

```

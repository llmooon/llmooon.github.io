---
layout: post
comments: true
categories: Algorithm
tag : 알고리즘
---

-  정렬 기준을 잘 고려하여 lis를 풀면 된다.
-  처음에는 접근 방법이 어려웠다. 
-  n^2 풀이

```c++
#include<iostream>
#include<vector>
#include<algorithm>
using namespace std;

typedef pair<int, int> p;
typedef pair<p, int> pp;
vector<pp> v;
vector<int> parent,dp;
int n,w,h,a,b,ans=1,ans_idx;
void go(int idx) {
	if (idx == -1) return;
	go(parent[idx]);
	printf("%d ", v[idx].second);
}
int main() {
	scanf("%d %d %d", &n, &w, &h);
	for (int i = 0; i < n; i++) {
		scanf("%d %d", &a,&b);
		if (a <= w) continue;
		if (b <= h) continue;
		v.push_back({ { a,-b } ,i+1});
	}
	parent.resize(n + 2,-1);
	dp.resize(n + 2, 1);
	sort(v.begin(), v.end());
	dp[0] = 1;
	parent[0] = -1;
	if (v.size() == 0) {
		printf("0");
		return 0;
	}
	for (int i = 1; i < v.size(); i++) {
		for (int j = 0; j < i; j++) {
			if (v[i].first.second < v[j].first.second) {
				if (dp[i] < dp[j] + 1) {
					dp[i] = dp[j] + 1;
					parent[i] = j;
				}
			}
		}
		if (ans < dp[i]) {
			ans = dp[i];
			ans_idx = i;
		}
	
	}
	printf("%d\n", ans);
	go(ans_idx);
	
}
```

- nlongn 풀이

- lis를 nlogn에 문제를 해결 하였다.

- (--it)->second와 --it->second 의 우선순위가 달라 결과가 바뀌는 issue가 있었다.

  ```c++
  #include<iostream>
  #include<vector>
  #include<algorithm>
  using namespace std;
  
  vector<pair<pair<int, int>, int>> v;
  vector<pair<int, int>> lis;
  vector<int> parent, dp;
  int n, w, h, a, b, ans = 1, ans_idx;
  void go(int idx) {
  	if (idx == -1) return;
  	go(parent[idx]);
  	printf("%d ", v[idx].second);
  }
  int main() {
  	scanf("%d %d %d", &n, &w, &h);
  	for (int i = 0; i < n; i++) {
  		scanf("%d %d", &a, &b);
  		if (a <= w) continue;
  		if (b <= h) continue;
  		v.push_back({ { a,-b } ,i + 1 });
  	}
  	parent.resize(n + 2, -1);
  	dp.resize(n + 2, 1);
  	sort(v.begin(), v.end());
  	dp[0] = 1;
  	parent[0] = -1;
  	if (v.size() == 0) {
  		puts("0");
  		return 0;
  	}
  	lis.push_back({ -v[0].first.second,0 });
  	for (int i = 1; i < v.size(); i++) {
  		if (lis.back().first < -v[i].first.second) {
  			parent[i] = lis.back().second;
  			lis.push_back({ -v[i].first.second,i });
  		}
  		else {
  			auto it = lower_bound(lis.begin(), lis.end(), make_pair(-v[i].first.second, -1));
  			*it = { -v[i].first.second, i };
  			if (it == lis.begin()) parent[i] = -1;
  			else parent[i] = (--it)->second;
  		}
  	}
  	printf("%d\n", lis.size());
  	go(lis.back().second);
  
  }
  ```


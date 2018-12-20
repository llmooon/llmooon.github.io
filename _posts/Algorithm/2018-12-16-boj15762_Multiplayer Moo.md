---
layout: post
comments: true
categories: Algorithm
tag : 알고리즘_BFS, 알고리즘_그래프압축
---

##  백준 15762 Multiplayer Moo

- n*n 그리드에 수 2개로 이루어진 연속된 제일 큰 구간 size 구하기
- 그래프 압축을 통해 시간 단축
  BFS를 하면서 (노드 i,노드 j) 선을 방문 했냐 안했냐로 알수 있음. => 연속된 수 2개로 이루어진 구간이기 떄문에 가능
- 2,3으로 연결된 구간인가에 대한 선과 2,4로 연결된 구간에 대한 선과의 중복이 없기 때문
  노드로 방문 했냐 안했냐가 아닌 간선으로 했냐 안했냐로 시간 줄인다.

```c++
#include<iostream>
#include<vector>
#include<algorithm>
#include<queue>
#include<set>
#include<time.h>

using namespace std;

int n, arr[250][250], clu[250][250], clu2[250][250], ans;
struct node {
	int num;
	int size;
	set<pair<int, int> > list;
};
vector<node> v;
queue<pair<int, int> > q;
set<pair<int, int> > bb;
int dx[4] = { 0,0,1,-1 }, dy[4] = { 1,-1,0,0 }, cnt = 1;
void bfs(int i, int j, int num, int mom) {
	q.push({ i,j });
	while (!q.empty()) {
		int nowx = q.front().first, nowy = q.front().second;
		q.pop();
		for (int i = 0; i < 4; i++) {
			int nx = nowx + dx[i], ny = nowy + dy[i];
			if (0 <= nx && nx < n && 0 <= ny && ny < n) {
				if (clu[nx][ny] == 0 && arr[nx][ny] == mom) {
					q.push({ nx,ny });
					clu[nx][ny] = num;
					cnt++;
				}
			}
		}
	}
}

void bfs2(int i, int j, int mom) {

}

int main() {
	scanf("%d", &n);
	for (int i = 0; i < n; i++) {
		for (int j = 0; j < n; j++) {
			scanf("%d", &arr[i][j]);
		}
	}
	int num = 1;
	clock_t s1, e1;
	s1 = clock();
	node newnode;
	v.push_back(newnode);
	for (int i = 0; i < n; i++) {
		for (int j = 0; j < n; j++) {
			if (clu[i][j] == 0) {
				clu[i][j] = num;
				bfs(i, j, num, arr[i][j]);
				node newnode;
				v.push_back(newnode);
				v[num].num = arr[i][j], v[num].size = cnt;
				num++, cnt = 1;
			}
		}
	}

	for (int i = 0; i < n; i++) {
		for (int j = 0; j < n; j++) {
			if (clu2[i][j] == 0) {
				clu2[i][j] = 1;
				int mom = clu[i][j];

				q.push({ i,j });
				while (!q.empty()) {
					int nowx = q.front().first, nowy = q.front().second;
					q.pop();
					for (int i = 0; i < 4; i++) {
						int nx = nowx + dx[i], ny = nowy + dy[i];
						if (0 <= nx && nx < n && 0 <= ny && ny < n) {
							if (clu[nx][ny] == mom) {
								if (clu2[nx][ny] == 0) {
									q.push({ nx,ny });
									clu2[nx][ny] = 1;
								}
							}
							else {
								v[mom].list.insert({ arr[nx][ny],clu[nx][ny] });
							}
						}
					}
				}

			}
		}
	}



	queue<int> pq;
	int mx2 = 0;

	for (int i = 1; i < v.size(); i++) {
		set<int> visit;
		visit.insert(v[i].num); // 이 번호를 찾은적 있는가?
		ans = max(ans, v[i].size);
		int num1 = v[i].num, num2;
		for (int j = 0; j < v[i].list.size(); j++) {
			auto now = v[i].list.begin();
			if (visit.find(now->first) != visit.end()) continue;
			if (bb.find({ min(i,now->second),max(i,now->second) }) != bb.end()) continue;
			bb.insert({ min(i,now->second),max(i,now->second) });
			num2 = now->first;
			visit.insert(num2);
			set<int> print;
			pq.push(i);
			int tmp = v[i].size;
			print.insert(i);
			while (!pq.empty()) {
				int now = pq.front();
				pq.pop();
				auto iter = v[now].list.lower_bound({ num1,0 });
				while (iter != v[now].list.end() && iter->first == num1) {
					if (print.find(iter->second) == print.end()) {
						print.insert(iter->second);
						bb.insert({ min(now,iter->second),max(now,iter->second) });
						pq.push(iter->second);
						tmp += v[iter->second].size;
						iter++;
					}
					else iter++;
				}
				iter = v[now].list.lower_bound({ num2,0 });
				while (iter != v[now].list.end() && iter->first == num2) {
					if (print.find(iter->second) == print.end()) {
						print.insert(iter->second);
						pq.push(iter->second);
						bb.insert({ min(now,iter->second),max(now,iter->second) });
						tmp += v[iter->second].size;
						iter++;
					}
					else iter++;
				}
			}
			mx2 = max(mx2, tmp);
			print.clear();
		}
		visit.clear();

	}

	e1 = clock();
	//printf("%.5f\n", ((float)e1 - s1) / CLOCKS_PER_SEC);
	printf("%d\n%d", ans, mx2);
}
```
---
layout: post
comments: true
categories: Algorithm
tag : 알고리즘
---

-  Bfs/ Dfs

```c++
#include<iostream>
#include<queue>
using namespace std;

char arr[110][110];
int color[26], visit[110][110], dx[4] = { 1,-1,0,0 }, dy[4] = { 0,0,1,-1 };
queue<pair<int, int> > q;

int main() {
	int n, m;
	char king;

	scanf("%d %d %c", &n, &m, &king);
	
	for (int i = 0; i < n; i++) {
		for (int j = 0; j < m; j++) {
			scanf(" %c", &arr[i][j]);
			if (arr[i][j] == king) {
				q.push({ i,j });
				visit[i][j] = 1;
			}
		}
	}
	
	int ans = 0;
	while (!q.empty()) {
		int r = q.front().first, c = q.front().second;
		q.pop();
		for (int i = 0; i < 4; i++) {
			int nr = r + dx[i], nc = c + dy[i];
			if (0 <= nr && nr < n && 0 <= nc && nc < m) {
				if (visit[nr][nc] == 0 && arr[nr][nc]!='.') {
					visit[nr][nc] = 1;
					if (color[arr[nr][nc] - 'A'] == 0) {
						ans++;
						color[arr[nr][nc] - 'A'] = 1;
					}
				}
			}
		}
	}
	printf("%d", ans);
	return 0;
}
```

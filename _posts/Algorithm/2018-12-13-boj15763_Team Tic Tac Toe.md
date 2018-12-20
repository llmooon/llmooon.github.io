---
layout: post
comments: true
categories: Algorithm
tag : 알고리즘_구현
---

## 백준 15763 Team Tic Tac Toe

쉬운 틱택토 구현

```c++
#include<iostream>
#include<set>
#include<algorithm>
using namespace std;
char arr[3][3];
set<char> s;
set<pair<int, int>> s2;
void add(int f1, int f2) {
	if (f1 > f2) swap(f1, f2);
	s2.insert({ f1,f2 });
}
int main() {
	char c;
	int ans1 = 0, ans2 = 0;
	for (int i = 0; i < 3; i++) {
		for (int j = 0; j < 3; j++) {
			scanf(" %c", &arr[i][j]);
		}
	}
	for (int i = 0; i < 3; i++) {
		if (arr[i][0] == arr[i][1] && arr[i][1] == arr[i][2]) s.insert(arr[i][1]);
		else if (arr[0][i] == arr[1][i] && arr[1][i] == arr[2][i]) s.insert(arr[1][i]);
	}
	if (arr[0][0] == arr[1][1] && arr[1][1] == arr[2][2]) s.insert(arr[0][0]);
	if (arr[2][0] == arr[1][1] && arr[1][1] == arr[0][2]) s.insert(arr[0][2]);

	for (int i = 0; i < 26; i++) {
		for (int j = i + 1; j < 26; j++) {
			int flag3 = 0, flag4 = 0;
			int f3 = -1, f33 = -1, f4 = -1, f44 = -1;
			for (int a = 0; a < 3; a++) {
				int flag1 = 0, flag2 = 0;
				int f1=-1, f11=-1, f2=-1, f22=-1;
				for (int b = 0; b < 3; b++) {
					if (arr[a][b] == 'A' + i || arr[a][b] == 'A' + j) { if (f1 == -1 || f1 ==arr[a][b]) f1 = arr[a][b]; else f11 = arr[a][b]; flag1++; }
					if (arr[b][a] == 'A' + j || arr[b][a] == 'A' + i) { if (f2 == -1 || f2 == arr[b][a]) f2 = arr[b][a]; else f22 = arr[b][a]; flag2++; }
				}
				if (arr[a][a] == 'A' + i || arr[a][a] == 'A' + j) { if (f3 == -1 || f3==arr[a][a]) f3 = arr[a][a]; else f33 = arr[a][a]; flag3++; }
				if (arr[a][2 - a] == 'A' + i || arr[a][2 - a] == 'A' + j) { if (f4 == -1 || f4==arr[a][2-a]) f4 = arr[a][2 - a]; else f44 = arr[a][2 - a]; flag4++; }
				if (flag1 == 3 && f11!=-1) 
					s2.insert({ i,j });
				if (flag2 == 3 && f22!=-1) 
					s2.insert({ i,j });
			}
			if (flag3 == 3 && f33 !=-1) 
				s2.insert({ i,j });
			if (flag4 == 3 && f44!=-1) 
				s2.insert({ i,j });

		}
	}
	printf("%d\n%d", s.size(), s2.size());
}

```
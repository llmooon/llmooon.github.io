---
layout: post
comments: true
categories: Algorithm
tag : 알고리즘_자료구조, 알고리즘_Map
---

-  map 을 사용하여 문제를 잘 사용하여 해결 할 수 있는 문제!

```c++
#include<iostream>
#include<map>
#include<string>
using namespace std;

map<string, int> m;
int n;
int main() {
	ios::sync_with_stdio(0);
	cin.tie(0);
	cin >> n;
	string s;
	for (int i = 0; i < n; i++) {
		cin >> s;
		auto finder = m.find(s);
		if (finder != m.end()) cout << s << finder->second++<<endl;
		else { 
			cout << "OK"<<endl; 
			m.insert({ s,1 });
		}
	}
}
```
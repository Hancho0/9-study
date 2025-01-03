[ 큐(Queue) ]

큐(Queue)는 선입선출(FIFO, First-In-First-Out) 자료구조를 구현하는 컨테이너 클래스이다.<br>
큐는 데이터를 삽입하는 enqueue와 데이터를 삭제하는 dequeue 연산을 지원한다.

[ 큐(Queue)의 특징 ]<br>
1. 선입선출(FIFO) 구조 : 선입선출 구조를 가지고 있어, 먼저 들어온 데이터가 먼저 처리되고 나중에 들어온 데이터는 나중에 처리된다.<br>
2. 제한적인 데이터 삽입/삭제 : 데이터를 삽입하는 경우는 큐의 맨 뒤에 새로운 데이터를 추가하고, 데이터를 삭제하는 경우는 큐의 맨 앞에서 데이터를 삭제한다.<br>
3. O(1)의 시간 복잡도 : 삽입과 삭제가 각각 O(1)의 시간 복잡도를 가지고 있어 효율적인 처리가 가능하다.<br>
4. 순차적인 접근 : 순차적인 접근만 가능하며, 임의의 위치에 있는 데이터에는 직접적으로 접근할 수 없다.

| 멤버 함수 | |
|---|---|
| q.push() | 큐의 뒤쪽에 데이터 삽입 |
| q.pop() | 큐의 맨 앞쪽의 데이터 제거 |
| q.front() | 큐의 맨 앞쪽의 데이터 반환 |
| q.back() | 큐의 맨 뒤쪽의 데이터 반환 |
| q.empty() | 큐가 비어 있는지 확인(비었으면 1, 아니면 0을 반환) |
| q.size() | 큐에 저장된 데이터의 개수 반환 |
| q.swap() | 서로 다른 두 큐의 데이터를 교환 할 때 사용 |

```ruby
#include <iostream>
#include <queue>

using namespace std;

int main() {
	queue<int> q;

	for (int i = 1; i <= 10; i++) {
		q.push(i);
	}

	while (!q.empty()) {
		int num = q.front();
		q.pop();

		if (num % 2 == 1) {
			cout << num << " ";
		}
	}

	cout << endl;

	return 0;
}
```

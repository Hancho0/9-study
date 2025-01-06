#LinkedList로 구현한 Queue

```ruby
#include <iostream>

using namespace std;

class NODE {
	int nData; // 노드의 데이터 필드 부분이다. (일반 변수)
	NODE *Link; // 노드의 링크 필드 부분이다. (포인터 변수)
public:
	NODE(int val) { nData = val; Link = NULL; } // 생성자이다. 파라미터로 변수 값을 받는다.
	NODE *getLink() { return Link; } // 포인터 변수인 Link에 저장된 다음 노드의 주소를 반환한다.

	void setLink(NODE *Next) { // 다음 노드의 주소를 저장하는 포인터 변수인 Link에 Next값이 저장된다.
		Link = Next;
	}
	void Display() { // 현재 노드의 데이터 필드(data)에 저장된 값을 출력한다.
		cout << nData << endl;
	}
};

class LinkedQueue {
	NODE *Front; // 노드의 주소를 갖는 포인터 변수 (큐의 처음)
	NODE *Rear; // 노드의 주소를 갖는 포인터 변수 (큐의 끝)
public:
	LinkedQueue() { // 생성자 큐의 Front와 Rear에 공백 문자열을 저장.
		Front = NULL; Rear = NULL;
	}
	~LinkedQueue() { // 삭제 생성자. 큐가 공백이 아니라면 while문을 반복한다.
		while (!isEmpty())
			delete Dequeue(0);
	}

	bool isEmpty() { // 큐가 비었는지를 반환하는 함수.
		return Front == NULL;
	}

	void Enqueue(NODE *p) { // 큐의 삽입 연산
		if (isEmpty())
			Front = Rear = p;
		else {
			Rear->setLink(p);
			Rear = p;
		}
	}

	NODE *Dequeue(NODE *p) { //큐의 삭제 연산
		if (isEmpty())
			return NULL;

		NODE *Temp = Front;
		Front = Front->getLink();

		if (Front == NULL)
			Rear = NULL;

		return Temp;
	}

	NODE *peek() { return Front; }

	void Display() {
		cout << "[큐 내용]: " << endl;
		for (NODE *p = Front; p != NULL; p = p->getLink())
			p->Display();
		cout << endl;
	}
};

void main() {
	LinkedQueue Que;
	for (int i = 1; i < 10; i++)
		Que.Enqueue(new NODE(i));
	Que.Display();
	
	delete Que.Dequeue(0);
	delete Que.Dequeue(0);
	delete Que.Dequeue(0);
	Que.Display();
	cout << Que.peek() << endl;
}
```

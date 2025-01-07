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


[ Queue.h ]

```ruby
#pragma once
class Queue
{
private:

	int myQueue[1000] = { 0, };
	int num = 0; //큐에 담긴 값의 갯수
	int* firstNum = nullptr; // 첫번째 값의 포인터

public:

	Queue();
	void Init();
	void EnQueue(int value);
	int DeQueue();
	bool IsEmpty();
	void Clear();
	int Count();

};
```

[ Queue.cpp ]

```ruby
#include "Queue.h"

Queue::Queue()
{
    Init();
}

void Queue::Init()
{
    firstNum = &myQueue[0];
}

void Queue::EnQueue(int value)
{
    myQueue[num++] = value;
}

int Queue::DeQueue()
{
    if (IsEmpty())
    {
        return -1;
    }

    int value = *firstNum;

    for (int i = 0; i < num-1; i++)
    {
        myQueue[i] = myQueue[i + 1];
    }

    num--;

    return value;
}

bool Queue::IsEmpty()
{
    if (num == 0)
        return true;
    else
        return false;
}

void Queue::Clear()
{
    num = 0;
}

int Queue::Count()
{
    return num;
}
```

[ main ]

```ruby
#include <iostream>
#include "Queue.h"
using namespace std;

int main()
{
	Queue queue;

	cout << "비어있는지 체크(0 - false / 1 - true)" << endl;
	cout << queue.IsEmpty() << endl;

	queue.EnQueue(3);
	queue.EnQueue(6);
	queue.EnQueue(9);

	cout << "\nEnqueue하고 비어있는지 체크(0 - false / 1 - true)" << endl;
	cout << queue.IsEmpty() << endl;

	cout << "\n제일 처음넣은 수 3" << endl;
	cout <<  queue.DeQueue() << endl;

	cout << "\n두번째 수 6" << endl;
	cout << queue.DeQueue() << endl;
	
	queue.Clear();

	cout << "\n클리어하고 비어있는지 체크(0 - false / 1 - true) " << endl;
	cout << queue.IsEmpty() << endl;
	
}
```



```ruby
#include<iostream>

const int MAXValue = 101;

using namespace std;

template<class T> class Queue
{
public:
	int Front;
	int Rear;
	int nSize;
	T *Values;

	Queue()
	{
		nSize = MAXValue;
		Values = new T[nSize];
		Front = 0;
		Rear = 0;
	}
	~Queue()
	{
		delete[] Values;
	}

	void Push(T Value)
	{
		if (!isFull())
		{
			Values[Rear] = Value;
			Rear = (Rear + 1) % nSize;
		}
		else
			cout << "큐가 꽉 찼습니다." << endl;
	}

	void Pop()
	{
		if (!empty())
			Front = (Front + 1) % nSize;
		else
			cout << "큐가 비어있습니다." << endl;
	}

	bool empty()
	{
		if (Rear == Front)
			return true;
		else
			return false;
	}

	bool isFull()
	{
		if ((Rear + 1) % nSize == Front)
			return true;
		else
			return false;
	}
};

template<typename T>
ostream& operator <<(ostream &out, Queue<T> &q) {
	T *Temp = q.Values;
	out << "front [ ";
	for (int i = q.Front; i < q.Rear; i++) {
		out << Temp[i];
		if (i < q.Rear - 1) out << " | ";
	}
	out << " ] rear" << endl;
	return out;
}

int main()
{
	Queue<int> q;
	q.Push(3);
	cout << q;
	q.Push(103);
	cout << q;
	q.Push(57);
	cout << q;
	q.Pop();
	cout << q;
	q.Push(22);
	cout << q;
	q.Pop();
	cout << q;
	q.Pop();
	cout << q;
	q.Pop();
	cout << q;
	q.Pop();
	cout << q;
}
```

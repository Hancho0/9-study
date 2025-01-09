```ruby
#include <iostream>
using namespace std;

template <typename T> class Queue 
{

private:
	size_t m_Front;
	size_t m_Rear;
	size_t m_Capacity;
	T *pArr;

public:
	Queue() 
	{

		m_Front = 0;
		m_Rear = 0;
		m_Capacity = 10;
		pArr = new T[m_Capacity];

	}

	bool Full() 
	{

		return m_Front == ( m_Rear + 1 ) % m_Capacity;

	}

	bool Empty() 
	{

		return m_Front == m_Rear;

	}

	void EnQueue( const T&& Data ) 
	{

		if ( !Full() ) 
		{
			
			pArr[m_Rear] = move(Data);
			m_Rear = (m_Rear + 1) % m_Capacity;

		}

	}

	T DeQueue() 
	{

		if (!Empty() ) 
		{

			T p = pArr[m_Front];
			m_Front = (m_Front + 1) % m_Capacity;
			return p;

		}

	}

	void Print() 
	{

		if ( m_Front > m_Rear ) 
		{

			for ( int i = m_Front; i < m_Capacity; i++ )
				cout << pArr[i] << ' ';

			for ( int i = 0; i < m_Rear; i++ )
				cout << pArr[i] << ' ';
			
		}

		else
		{

			for (int i = m_Front; i < m_Rear; i++)
				cout << pArr[i] << ' ';

		}

	}

};

int main() {
	Queue<int> q;

	q.EnQueue(10);
	q.EnQueue(20);
	q.EnQueue(30);

	cout << "초기 큐 상태: ";
	q.Print();
	cout << endl;

	int outValue = q.DeQueue();
	cout << "DeQueue한 값: " << outValue << endl;

	cout << "DeQueue 1회 후 큐 상태: ";
	q.Print();
	cout << endl;

	for (int i = 1; i <= 7; i++) {
		q.EnQueue(i * 100);
	}
	cout << "추가 EnQueue 후 큐 상태: ";
	q.Print();
	cout << endl;

	for (int i = 0; i < 3; i++) {
		cout << "DeQueue: " << q.DeQueue() << endl;
	}
	cout << "3회 DeQueue 후 큐 상태: ";
	q.Print();
	cout << endl;

	q.EnQueue(999);
	q.EnQueue(1000);
	cout << "추가 EnQueue(999, 1000) 후 큐 상태: ";
	q.Print();
	cout << endl;

	return 0;
}
```

-----

```ruby
#include<iostream>

const int MAXValue = 101;

using namespace std;

template<class T> class Queue
{

public:
	int m_Front;
	int m_Rear;
	int m_nSize;
	T *pValues;

	Queue()
	{

		m_nSize = MAXValue;
		pValues = new T[m_nSize];
		m_Front = 0;
		m_Rear = 0;

	}
	~Queue()
	{

		delete[] pValues;

	}

	void Push( T Value )
	{

		if ( !isFull() )
		{

			pValues[m_Rear] = Value;
			m_Rear = (m_Rear + 1) % m_nSize;

		}

		else
			cout << "큐가 꽉 찼습니다." << endl;

	}

	void Pop()
	{

		if ( !empty() )
			m_Front = (m_Front + 1) % m_nSize;

		else
			cout << "큐가 비어있습니다." << endl;

	}

	bool empty()
	{

		if ( m_Rear == m_Front )
			return true;

		else
			return false;

	}

	bool isFull()
	{
		if ( (m_Rear + 1) % m_nSize == m_Front )
			return true;

		else
			return false;

	}

};

template<typename T>
ostream& operator <<(ostream &out, Queue<T> &q) 
{

	T *temp = q.pValues;

	out << "front [ ";

	for ( int i = q.m_Front; i < q.m_Rear; i++ ) 
	{

		out << temp[i];

		if ( i < q.m_Rear - 1 ) 
			out << " | ";

	}

	out << " ] rear" << endl;

	return out;

}
```

-----

```ruby
#include <iostream>

using namespace std;

class NODE {
	int nData; // 노드의 데이터 필드 부분이다. (일반 변수)
	NODE *pLink; // 노드의 링크 필드 부분이다. (포인터 변수)

public:
	NODE( int val ) { nData = val; pLink = NULL; } // 생성자이다. 파라미터로 변수 값을 받는다.
	NODE *pGetLink() { return pLink; } // 포인터 변수인 Link에 저장된 다음 노드의 주소를 반환한다.

	void setLink( NODE *Next ) // 다음 노드의 주소를 저장하는 포인터 변수인 Link에 Next값이 저장된다.
	{ 

		pLink = Next;

	}
	void Display() // 현재 노드의 데이터 필드(data)에 저장된 값을 출력한다.
	{ 

		cout << nData << endl;

	}
};

class LinkedQueue 
{

	NODE *m_Front; // 노드의 주소를 갖는 포인터 변수 (큐의 처음)
	NODE *m_Rear; // 노드의 주소를 갖는 포인터 변수 (큐의 끝)

public:
	LinkedQueue() // 생성자 큐의 Front와 Rear에 공백 문자열을 저장.
	{ 

		m_Front = NULL; m_Rear = NULL;

	}
	~LinkedQueue() // 삭제 생성자. 큐가 공백이 아니라면 while문을 반복한다.
	{ 

		while ( !isEmpty() )
			delete Dequeue(0);

	}

	bool isEmpty() // 큐가 비었는지를 반환하는 함수.
	{ 

		return m_Front == NULL;

	}

	void Enqueue( NODE *p ) // 큐의 삽입 연산
	{ 

		if ( isEmpty() )
			m_Front = m_Rear = p;

		else 
		{

			m_Rear->setLink(p);
			m_Rear = p;

		}

	}

	NODE *Dequeue( NODE *p ) //큐의 삭제 연산
	{ 

		if ( isEmpty() )
			return NULL;

		NODE *Temp = m_Front;
		m_Front = m_Front->pGetLink();

		if ( m_Front == NULL )
			m_Rear = NULL;

		return Temp;

	}

	NODE *peek() { return m_Front; }

	void Display() 
	{

		cout << "[큐 내용]: " << endl;

		for (NODE *p = m_Front; p != NULL; p = p->pGetLink())
			p->Display();

		cout << endl;

	}

};
```

```ruby
#include <iostream>
using namespace std;

struct NODE
{
	int nData;
	NODE *pNext;
};

class LinkedList {
	NODE *m_Head;
	NODE *m_Tail;

public:
	LinkedList() : m_Head(NULL) {}

	void InsertFirst( int nValue ) {

		NODE *pNewNode = new NODE();
		pNewNode->nData = nValue;
		pNewNode->pNext = m_Head;
		m_Head = pNewNode;

		if ( !m_Tail ) 
		{

			m_Tail = pNewNode;

		}

	}

	void InsertLast( int nValue ) 
	{

		NODE *pNewNode = new NODE();
		pNewNode->nData = nValue;
		pNewNode->pNext = NULL;

		if ( !m_Head ) 
		{

			m_Head = pNewNode;
			m_Tail = pNewNode;
			return;

		}
		m_Tail->pNext = pNewNode;
		m_Tail = pNewNode;

	}

	void InsertPosition( int nValue, int nPosition ) 
	{

		if ( nPosition < 1 ) 
		{

			cout << "위치가 1보다는 커야합니다." << endl;
			return;

		}

		if ( nPosition == 1 ) 
		{

			InsertFirst( nValue );
			return;

		}

		NODE *pNewNode = new NODE();
		pNewNode->nData = nValue;

		NODE *m_pCurrent = m_Head;
		for ( int i = 1; i < nPosition - 1 && m_pCurrent; ++i ) 
		{

			m_pCurrent = m_pCurrent->pNext;

		}

		if ( !m_pCurrent ) 
		{

			cout << "위치가 범위를 벗어났습니다." << endl;
			delete pNewNode;
			return;

		}

		pNewNode->pNext = m_pCurrent->pNext;
		m_pCurrent->pNext = pNewNode;

	}

	void DeleteFirst() 
	{

		if ( !m_Head ) 
		{

			cout << "리스트가 비어있습니다." << endl;
			return;

		}

		NODE *m_pCurrent = m_Head;
		m_Head = m_Head->pNext;
		delete m_pCurrent;

	}

	void DeleteLast() 
	{

		if ( !m_Head ) 
		{

			cout << "리스트가 비었습니다." << endl;
			return;

		}

		if ( !m_Head->pNext ) 
		{

			delete m_Head;
			m_Head = NULL;
			return;

		}

		NODE *m_pCurrent = m_Head;
		while ( m_pCurrent->pNext->pNext ) 
		{

			m_pCurrent = m_pCurrent->pNext;

		}

		delete m_pCurrent->pNext;
		m_pCurrent->pNext = NULL;

	}

	void DeletePositon(int nPosition) 
	{

		if ( nPosition < 1 ) 
		{

			cout << "위치가 1보다는 커야합니다." << endl;
			return;

		}

		if ( nPosition == 1 ) 
		{

			DeleteFirst();
			return;

		}

		NODE *m_pCurrent = m_Head;
		for ( int i = 1; i < nPosition - 1 && m_pCurrent; i++ ) 
		{

			m_pCurrent = m_pCurrent->pNext;

		}

		if ( !m_pCurrent || !m_pCurrent->pNext ) 
		{

			cout << "위치가 범위를 벗어났습니다." << endl;

		}

		NODE *NodeToDelete = m_pCurrent->pNext;
		m_pCurrent->pNext = m_pCurrent->pNext->pNext;
		delete NodeToDelete;

	}

	void Display() 
	{

		if ( !m_Head ) 
		{

			cout << "리스트가 비어있습니다." << endl;
			return;

		}

		NODE *pCurrent = m_Head;
		while ( pCurrent ) 
		{

			cout << pCurrent->nData << " -> ";
			pCurrent = pCurrent->pNext;

		}
		cout << "NULL" << endl;

	}

};

#include <iostream>
using namespace std;

int main() {
	LinkedList List;

	cout << "리스트 앞에 요소 삽입: 10, 20, 30" << endl;
	List.InsertFirst(10);
	List.InsertFirst(20);
	List.InsertFirst(30);
	List.Display();

	cout << "\n리스트 뒤에 요소 삽입: 40, 50" << endl;
	List.InsertLast(40);
	List.InsertLast(50);
	List.Display();

	cout << "\n리스트의 3번째 위치에 25 삽입" << endl;
	List.InsertPosition(25, 3);
	List.Display();

	cout << "\n리스트 첫 번째 요소 삭제" << endl;
	List.DeleteFirst();
	List.Display();

	cout << "\n리스트 마지막 요소 삭제" << endl;
	List.DeleteLast();
	List.Display();

	cout << "\n리스트의 2번째 위치 요소 삭제" << endl;
	List.DeletePositon(2);
	List.Display();

	return 0;
}
```

-----

```ruby
#pragma once
#include <iostream>
using namespace std;

struct NODE
{

	int nData;
	struct NODE *Link;

};

struct HeadNode 
{

	NODE *Head;
	NODE *Tail;

};

class SingList 
{

public:
	HeadNode *CreateList() 
	{

		HeadNode* H = new HeadNode;
		H->Head = NULL;
		H->Tail = NULL;
		return H;

	}

	void AddNode( HeadNode *H, int x ) 
	{

		NODE *NewNode = new NODE;
		NODE *LastNode;
		NewNode->nData = x;
		NewNode->Link = NULL;

		if ( H->Head == NULL ) 
		{

			H->Head = NewNode;
			H->Tail = NewNode;
			return;

		}

		H->Tail->Link = NewNode;
		H->Tail = NewNode;

	}
	void DeleteNode( HeadNode *H ) 
	{

		NODE *PrevNode;
		NODE *DelNode;

		if ( H->Head == NULL ) 
			return;
		if ( H->Head->Link == NULL ) 
		{

			delete H->Head;
			H->Head = NULL;
			return;

		}
		else 
		{

			PrevNode = H->Head;
			DelNode = H->Head->Link;

			while ( DelNode->Link != NULL ) 
			{

				PrevNode = DelNode;
				DelNode = PrevNode->Link;

			}

			free( DelNode );
			PrevNode->Link = NULL;

		}

	}

	void DeleteThisNode( HeadNode *H, int nDelData ) 
	{

		NODE *DelNode;
		NODE *PrevNode;
		PrevNode = H->Head;

		while ( PrevNode->Link->nData != nDelData ) 
		{

			PrevNode = PrevNode->Link;

		}

		DelNode = PrevNode->Link;
		PrevNode->Link = DelNode->Link;
		free(DelNode);

		cout << nDelData << " 데이터 값을 가진 노드가 삭제되었습니다. " << endl;
		return;
	}

	void AddThisNode( HeadNode *H, int nAfterThisData, int nAddData ) 
	{

		NODE *PrevNode;
		PrevNode = H->Head;

		while ( PrevNode->nData != nAfterThisData ) 
		{

			PrevNode = PrevNode->Link;

		}

		NODE *NewNode = new NODE;

		NewNode->nData = nAddData;
		NewNode->Link = PrevNode->Link;
		PrevNode->Link = NewNode;
		return;
	}

	void SearchNode( HeadNode *H, int nThisData ) 
	{

		NODE *SomeNode;
		SomeNode = H->Head;

		while ( SomeNode->nData != nThisData ) 
		{

			SomeNode = SomeNode->Link;

		}

		cout << nThisData << " 데이터를 검색하는 데 성공했습니다. " << endl;

	}

	void PrintList( HeadNode *L ) 
	{

		NODE *p;
		cout << " 연결리스트 목록 = ( ";
		p = L->Head;

		while ( p != NULL ) 
		{

			cout << p->nData;
			p = p->Link;
			if ( p != NULL ) 
				cout << " --> ";

		}

		cout << " )" << endl;

	}

};
```

-----

```ruby
#include <iostream>
using namespace std;

template<typename T> struct NODE
{

	T Data;
	NODE<T> *Next;
	NODE( const T& a, NODE *n ) : Data(a), Next(n) {}

};

template<typename T> class sList 
{

private:
	NODE<T> *m_Head;
	NODE<T> *m_Tail;
	NODE<T> *m_pCurrent;

public:
	sList() : m_Head(0) {}

	void Push_Front( const T& a )
	{

		m_Head = new NODE<T>(a, m_Head);

		if ( m_Tail == nullptr ) 
		{

			m_Tail = m_Head;

		}

	}

	void Push_Back( const T& a ) 
	{

		if ( m_Tail == nullptr ) 
		{

			m_Head = new NODE<T>( a, nullptr );
			m_Tail = m_Head;
			return;

		}

		m_Tail->Next = new NODE<T>( a, nullptr );
		m_Tail = m_Tail->Next;

	}

	NODE<T> *FindNode(const T& a) 
	{

		m_pCurrent = m_Head;

		while ( m_pCurrent != NULL ) 
		{

			if ( m_pCurrent->Data == a ) 
				return m_pCurrent;

			m_pCurrent = m_pCurrent->Next;

		}

		throw "값을 찾지 못했습니다.";

	}

	void AddAfter( NODE<T> *Prev_Node, const T& a ) 
	{

		Prev_Node->Next = new NODE<T>( a, Prev_Node->Next );

	}

	void DeleteAfter( NODE<T> *Prev_Node ) 
	{

		if ( Prev_Node->Next != NULL )
			Prev_Node->Next = Prev_Node->Next->Next;

	}

	void ListPrint() 
	{

		m_pCurrent = m_Head;

		while ( m_pCurrent != NULL ) 
		{

			cout << m_pCurrent->Data << ' ';
			m_pCurrent = m_pCurrent->Next;

		}

		cout << "\n";

	}

};
```

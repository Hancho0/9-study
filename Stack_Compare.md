```ruby
#include <iostream>
using namespace std;

template<typename T> class Stack 
{

private:
	T *pArr;
	unsigned int m_Capacity;
	unsigned int m_Size;

public:
	Stack() 
	{

		m_Capacity = 3;
		m_Size = 0;
		pArr = new T[m_Capacity];

	}

	~Stack() 
	{

		if ( pArr != NULL ) 
			delete[] pArr;

	}

	void ReSize() 
	{

		m_Capacity *= 2;

		T *pNewArr = new T[m_Size];

		for ( int i = 0; i < m_Size; i++ ) 
			pNewArr[i] = pArr[i];

		delete[] pArr;

		pArr = new T[m_Capacity];

		for ( int i = 0; i < m_Size; i++ ) 
			pArr[i] = pNewArr[i];

		delete[] pNewArr;

		pNewArr = nullptr;

	}

	void Push( T Data ) 
	{

		if ( m_Size >= m_Capacity ) 
		{

			ReSize();
		}

		pArr[m_Size++] = Data;

	}

	T Pop() 
	{

		if ( m_Size )
			return pArr[--m_Size];

		else
			throw out_of_range("스택이 비어있습니다.");

	}

	T Top() 
	{

		if  ( m_Size )
			return pArr[m_Size - 1];

		else
			throw out_of_range("스택이 비어있습니다.");

	}

	T Capacity() 
	{

		return m_Capacity;

	}

	T Size() 
	{

		return m_Size;

	}

	bool Empty() 
	{

		return m_Size == 0 ? true : false;

	}
};

int main() {
	Stack<int> stack;

	for ( int i = 1; i < 6; i++ ) 
	{

		stack.Push(i * 10);
		cout << "Push: " << i * 10 << endl;

	}

	cout << "스택 크기(Size): " << stack.Size() << endl;
	cout << "스택 용량(Capacity): " << stack.Capacity() << endl;
	cout << "스택이 비었나요? " << (stack.Empty() ? "Yes" : "No") << endl;

	cout << "Top(): " << stack.Top() << endl;

	cout << "Pop(): " << stack.Pop() << endl;
	cout << "Pop(): " << stack.Pop() << endl;
	cout << "스택 크기(Size): " << stack.Size() << endl;

	return 0;
}
```

-----

```ruby
#include <iostream>

using namespace std;

class myStack {

public:
	void Push( int nNum );
	void Pop();
	void Print();

private:
	int Arr[10] = { 0, };
	int Top = -1;
};

void myStack::Push( int nNum ) 
{

	if ( Top < 9 ) 
	{

		Top++;
		Arr[Top] = nNum;

	}

	else 
	{

		cout << "Stack is Full" << endl;

	}
}

void myStack::Pop() 
{

	if ( Top == -1 ) 
	{

		cout << "Stack is Empty" << endl;

	}

	else 
	{

		Arr[Top] = 0;
		Top--;

	}
}

void myStack::Print() 
{
	if ( Top == -1 ) {
		cout << "Stack is Empty" << endl;
	}
	else 
	{

		for ( int i = 0; i <= Top; i++ ) 
		{

			cout << i << " : " << Arr[i] << endl;

		}
		cout << endl;

	}
}
```

-----

```ruby
#include <iostream>

using namespace std;

const int SIZE = 100;

class Stack 
{

public:
	Stack() { Top = -1; }
	void Push( int nNum );
	int Pop();
	int isFull();
	int isEmpty();
	void printError( const char *msg );

private:
	int Arr[SIZE];
	int Top;
};

void Stack::Push( int nNum ) 
{

	Top += 1;

	if ( isFull() ) 
	{

		Top -= 1;
		printError("함수가 포화상태입니다.");

	}

	else
	{

		Arr[Top] = nNum;

	}

}

int Stack::Pop() 
{

	if ( isEmpty() ) 
	{

		printError("스택이 비었습니다.");
		return false;

	}

	else
		return Arr[Top--];
}

int Stack::isFull() 
{

	return Top >= SIZE ? true : false;

}

int Stack::isEmpty() 
{

	return Top == -1 ? true : false;

}

void Stack::printError( const char *msg ) 
{

	cout << "----- " << msg << "-----" << endl << endl;

}
```

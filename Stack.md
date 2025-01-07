[ 스택_Stack ]

* 자료의 **삽입** 과 **삭제**에 대한 규칙이 있는 자료구조 중 하나
* 가장 먼저 자료구에 **삽입(push)** 된 데이터가 제일 마지막에 **삭제(pop)** 됨
* 이를 선입후출(First In last Out) 혹은 후입선출(last In First Out)이라 함
* 또한 스택은 언제나 제일 위에 있는 자료만 접근 가능하다. **중간 자료에 임의 접근 안됨

```ruby
#include <iostream>

using namespace std;

class myStack {
public:
	void Push();
	void Pop();
	void Print();
private:
	int Arr[10] = { 0, };
	int Top = -1;
};

void myStack::Push() {
	if (Top < 9) {
		int nNum;
		cout << "숫자를 입력하세요 : " << endl;
		cin >> nNum;
		cout << endl;
		Top++;
		Arr[Top] = nNum;
	}
	else {
		cout << "Stack is Full" << endl;
	}
}

void myStack::Pop() {
	if (Top == -1) {
		cout << "Stack is Empty" << endl;
	}
	else {
		Arr[Top] = 0;
		Top--;
	}
}

void myStack::Print() {
	if (Top == -1) {
		cout << "Stack is Empty" << endl;
	}
	else {
		for (int i = 0; i <= Top; i++) {
			cout << i << " : " << Arr[i] << endl;
		}
		cout << endl;
	}
}

int main() {
	myStack stack;
	int nInput;

	while (1) {
		cout << "1. push / 2. pop / 3. print / 4. eixt" << endl << endl;
		cin >> nInput;
		cout << endl;
		switch (nInput) {
		case 1:
			stack.Push();
			break;

		case 2:
			stack.Pop();
			break;

		case 3:
			stack.Print();
			break;

		case 4:
			return 0;
		
		default:
			cout << "잘못된 입력입니다." << endl;
		}
	}
	return 0;
}
```

```ruby
#include <iostream>

using namespace std;

const int SIZE = 100;

class Stack {
public:
	Stack() { Top = -1; }
	void Push();
	int Pop();
	int isFull();
	int isEmpty();
	void printError(const char *msg);
private:
	int Arr[SIZE];
	int Top;
};

void Stack::Push() {
	Top += 1;
	if (isFull()) {
		Top -= 1;
		printError("함수가 포화상태입니다.");
	}
	else{
		int nItem;
		cout << "정수 : " << endl;
		cin >> nItem;
		Arr[Top] = nItem;
	}
}

int Stack::Pop() {
	if (isEmpty()) {
		printError("스택이 비었습니다.");
		return false;
	}
	else
		return Arr[Top--];
}

int Stack::isFull() {
	return Top >= SIZE ? true : false;
}

int Stack::isEmpty() {
	return Top == -1 ? true : false;
}

void Stack::printError(const char *msg) {
	cout << "----- " << msg << "-----" << endl << endl;
}

int main(void) {

	Stack stack;

	while (1) {
		int nInput;
		cout << "[push: 1  pop: 2  exit: 3]";
		cin >> nInput;

		if (nInput == 1) {
			stack.Push();
			cout << endl;
		}
		else if (nInput == 2) {
			int nBuff = stack.Pop();
			if (nBuff)
				cout << "Pop: " << nBuff << endl << endl;
		}
		else {
			break;
		}
	}
	return 0;

}
```

```ruby
#include <iostream>
using namespace std;

template<typename T> class Stack {
private:
	T* Arr;
	unsigned int m_Capacity;
	unsigned int m_Size;

public:
	Stack() {
		m_Capacity = 3;
		m_Size = 0;
		Arr = new T[m_Capacity];
	}

	~Stack() {
		if (Arr != NULL) delete[] Arr;
	}

	void ReSize() {
		m_Capacity *= 2;
		T *Tmp = new T[m_Size];
		for (int i = 0; i < m_Size; i++) Tmp[i] = Arr[i];

		delete[] Arr;
		Arr = new T[m_Capacity];
		for (int i = 0; i < m_Size; i++) Arr[i] = Tmp[i];
		delete[] Tmp;
		Tmp = nullptr;
	}

	void Push(T Data) {
		if (m_Size >= m_Capacity) {
			ReSize();
		}

		Arr[m_Size++] = Data;
	}

	T Pop() {
		if (m_Size)
			return Arr[--m_Size];
		else
			throw out_of_range("스택이 비어있습니다.");
	}

	T Top() {
		if (m_Size)
			return Arr[m_Size - 1];
		else
			throw out_of_range("스택이 비어있습니다.");
	}

	T Capacity() {
		return m_Capacity;
	}

	T Size() {
		return m_Size;
	}

	bool Empty() {
		return m_Size == 0 ? true : false;
	}
};

int main() {
	Stack<int> stack;

	stack.Push(10);
	stack.Push(20);
	stack.Push(30);

	cout << "스택 Top: " << stack.Top() << endl;         
	cout << "스택 Size: " << stack.Size() << endl;       
	cout << "스택 Capacity: " << stack.Capacity() << endl; 

	stack.Push(40);  
	cout << "스택 Size (추가 후): " << stack.Size() << endl;        
	cout << "스택 Capacity (추가 후): " << stack.Capacity() << endl; 

	cout << "Pop: " << stack.Pop() << endl;
	cout << "Pop: " << stack.Pop() << endl; 

	cout << "스택이 비었나요? " << (stack.Empty() ? "Yes" : "No") << endl;

	return 0;
}
```

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

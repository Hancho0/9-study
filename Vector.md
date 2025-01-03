[ 벡터(Vector ]

동적 배열으로, 크기를 동적으로 조절할 수 있는 데이터 구조이다.<br>
벡터는 배열과 비슷하지만, 배열과는 달라 크기를 미리 지정하지 않고 동적으로 조절할 수 있다. 즉, 프로그램 실행 중에 필요에 따라 배열의 크기를 늘리거나 줄일 수 있다.<br>
또한 벡터는 사용자가 데이터를 추가하거나 제거할 때 자랑으로 크기를 조절한다. 크기를 동적으로 조절함으로써 메모리를 효율적으로 활용할 수 있다. 원래 배열은 컴파일 시에 크기를 고정해야 하지만 벡터는 선언 시 크기를 지정하지 않아도 된다.<br>
따라서 실행 중에 필요에 따라 크기를 조절할 수 있어 더 유연한 데이터 구조를 제공한다.

추가적으로 벡터의 각 원소는 인덱스를 사용하여 접근이 가능하다. 예를 들어 myVector[0]은 첫 번째 원소를 나타낸다.<br>
배열은 선언할 때 크기를 지정하며, 이 크기는 컴파일 시에 고정된다. 배열의 크기를 변경하려면 새로운 배열을 생성하고 데이터를 복사해야 하나. 그렇지만 벡터는 동적으로 크기를 조절할 수 있다. 필요에 따라 원소를 추가하거나 삭제할 수 있고, 이로 인해 벡터의 크기가 동적으로 변한다.

벡터는 다양한 멤버 변수들을 제공한다. 예를 들어, push_back 함수를 사용하여 원소를 벡터의 끝에 추가할 수 있고, pop_back 함수로 마지막 원소를 삭제할 수 있다. 생각보다 간단하게 진행되는 장점이 있다. 벡터는 데이터 크기가 동적으로 변하는 상황에서 특히 유용하다. 예를 들어 데이터를 동적으로 수집하거나 다룰 때 효과적으로 사용할 수 있다.

1) 기본 선언 방법<br>
vector<데이터 타입> 이름; ex) vector<int> v;

2) 크기를 지정하여 선언<br>
vector<데이터 타입> 이름(크기); ex vector<int> v(5);

3) 크기와 초기값을 지정하여 선언<br>
vector<데이터 타입> 이름(크기,초기값); ex vector<int> v(5,0)

[ Vector 원소 접근하기 ]

|  | |
|---|---|
| v.size(); | 백터 v의 크기 반환 |
| v.front(); | 백터 v의 처음 값 반환 |
| v.back(); | 백터 v의 마지막 값 반환 |
| v[k]; | 인덱스 k 위치에 해당하는 값 반환 |
| v.at(k); | 인덱스 k 위치에 해당하는 값 반환 |
| v.begin(); | 처음 데이터의 위치 (인덱스 값) |
| v.end(); | 마지막 데이터의 다음 위치\n(=벡터의 마지막 원소의 인덱스 값 + 1) |

[ Vector 원소 삽입 ]

|  | |
|---|---|
| v.push_back(n) | 벡터 v의 마지막에 n을 삽입 |
| v.insert(v.begin() + k,n); | 벡터 v의 인덱스 k위치에 n을 삽입 |

[ Vector 원소 삭제 ]

|  | |
|---|---|
| v.pop_back(); | 벡터 v의 마지막 값 삭제 |
| v.erase(v.begin() + k); | 벡터 v의 인덱스 k위치에 해당하는 원소 삭제 |
| v.clear() | 벡터 v의 모든 원소 삭제 |


```ruby
#include <vector>
#include <iostream>

int main() {

  //백터 선언 및 초기값 선언
	std::vector<int> myVector = { 1,2,3,4,5 };

	myVector.push_back(6);
	myVector.push_back(7);

	myVector.pop_back();

	for (int value : myVector) {
		std::cout << value << " ";
	}

	return 0;
}
```

```ruby
#include <vector>
#include <iostream>

int main() {
	std::vector<std::vector<int>> matrix(3, std::vector<int>(3, 0));

	matrix[1][1] = 5;
	matrix[2][2] = 10;

	for (const auto& row : matrix) {
		for (int val : row) {
			std::cout << val << " ";
		}
		std::cout << std::endl;
	}

	return 0;
}
```

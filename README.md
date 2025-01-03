# 9-study

--------

Linked List 는 각 노드가 데이터와 포인터를 가지고 한 줄로 연결되어 있는 방식으로 데이터를 저장하는 자료 구조이다.

Linked List 는 단일 연결 리스트(Singly Linked list), 이중 연결 리스트(Doubly Linked List), 원형 연결 리스트(Circular Linked List)가 있다.

[ 연결리스트 ]

5 -> 17 -> 62 -> 2

만약 3번째 원소인 62를 찾고 싶다면 5를 지나서 17을 각, 17을 거쳐서 62를 가야한다.<br>
5는 자기 다음 차레가 17이라는 것만을 알고 있고, 17은 자기 다음 차레가 62라는 것만을 알고 있다. 따라서 5만 알고 있으면 17, 62, 2를 알아 낼 수 있다.

연결 리스트 성질<br>
1. n번째 원소를 확인하거나 변경하기 위해서 O(n)의 시간 복잡도가 필요하다.
2. 임의의 위치에 원소를 추가하거나 임의의 위치에 있는 원소를 제거하기 위해서 O(1)의 시간 복잡도가 필요하다.

[ 단일 연결 리스트 ]

5 -> 17 -> 62 -> 2

각각의 원소가 자신의 다음 원소의 주소를 들고 있다.

[ 이중 연결 리스트 ]

5 <-> 17 <-> 62 <-> 2

각가의 원소가 자신의 이전원소와 자신의 다음 원소의 주소를 모두 들고 있다.

[ 원형 연결 리스트 ]

5 -> 17 -> 62 -> 2<br>
^---------<------v

끝 원소와 처음 원소가 연결 되어 있다.


[ LinkedList.h 헤더파일 ]

```ruby
	struct Node
	{
		int data;
		Node* nextNode;
	};

	struct List
	{
		Node* headNode;
		Node* curNode;
	};
```

값과 다음 노드의 포인터를 가지고 있는 Node 라는 구조체와 headNode(리스트 맨 앞 노드) 포인터, curNode(현재 탐색 중인 노드) 포인터 가 있는 List 구조체를 만든다.

```ruby
class LinkedList
{
public:
	List* list;
	
	LinkedList(); //생성자
	void InitList(); //리스트 초기화

	Node* Find(List* list, Node* node); //같은 노드 찾기
	void InsertHeadNode(int value); //맨 앞에 노드 삽입
	void InsertTailNode(int value); //맨 끝에 노드 삽입
	void RemoveHeadNode(); //맨 앞 노드 삭제
	void RemoveTailNode(); //맨 끝 노드 삭제
	void RemoveCurNode(); //현재 선택한 노드 삭제
	void Clear(); //List 지우기
	void PrintCurNode(); //현재 선택 노드 출력
	void PrintAllNode(); //모든 노드 출력
};

[ LinkedList.cpp 파일 ]

```ruby
LinkedList::LinkedList()
{
	InitList();
}

void LinkedList::InitList()
{
	list = new List();
	list->curNode = nullptr;
	list->headNode = nullptr;
}
```

List 포인터 변수와 연결리스트의 기능을 담당할 많은 함수들을 선언


```ruby
void LinkedList::PrintCurNode()
{
	if (list->curNode != nullptr) {
		std::cout << "현재 노드 : " << list->curNode->data << std::endl;
	}
	else //현재 노드가 없다면
	{
		std::cout << "프린트curNode 함수 - 현재 노드가 없습니다!" << std::endl;
	}
}
```

현재 노드를 출력하는 함수에서는 리스트의 curNode를 검사해서 출력해주기만 했다.

```ruby
void LinkedList::PrintAllNode()
{

    if (list->headNode == nullptr) //노드가 하나도 없다면
    {
        std::cout << "프린트AllNode 함수 - 현재 노드가 하나도 없습니다!" << std::endl;
        return;
    }
        
    Node* tempNode = list->headNode;

    std::cout << "========= 전체노드 출력 시작 ==========" << std::endl;

    while (tempNode != nullptr)
    {
        std::cout << tempNode->data << std::endl;
        tempNode = tempNode->nextNode;
    }

    std::cout << "========= 전체노드 출력 끝 ==========" << std::endl;
}
```

모든 노드를 출력해야하는 PrintAllNode 함수에서는 반복할때마다 다음 노드를 tempNode에 대입해서 끝까지 반복하며 출력하게 만들었다.

```ruby
void LinkedList::InsertHeadNode(int value)
{
	Node* newNode = new Node();
	newNode->data = value;

	newNode->nextNode = list->headNode;
	list->headNode = list->curNode = newNode;
}
```

맨 앞 노드 삽입 함수 InserHeadNode 함수에는 노드를 생성해서 다음 노드에 현재 맨앞 노드를 넣어주고, 리스트의 현재 노드와 맨 앞노드에 생성한 노드를 넣어주었다.

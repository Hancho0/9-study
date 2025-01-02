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

5 -> 17 -> 62 -> 2
^---------<------v

끝 원소와 처음 원소가 연결 되어 있다.


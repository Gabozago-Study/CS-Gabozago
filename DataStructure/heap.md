# Heap

### Heap
- 완전 이진 트리(Complete Binary Tree)를 기반으로 한 자료 구조지만 중복을 허용.
- 부모 노드와 자식 노드 간의 우선순위를 비교하여 최대 값 또는 최소 값이 항상 루트 노드에 위치하도록 유지
- 최대 값 또는 최소 값에 빠르게 접근할 수 있어 최대/최소 우선순위를 갖는 요소에 대한 검색과 삭제가 효율적이다
- 삽입 및 삭제 작업 시간 복잡도가 O(log n)으로 일정하다
- 단, 임의의 요소에 접근하는 데는 효율적이지 않다. 선형 검색이 필요하며, O(n)의 시간 복잡도를 가진다

### 최대 힙(max heap)
- 부모 노드의 키 값이 자식 노드의 키 값보다 크거나 같은 완전 이진 트리
- key(부모 노드) >= key(자식 노드)
### 최소 힙(min heap)
- 부모 노드의 키 값이 자식 노드의 키 값보다 작거나 같은 완전 이진 트리
- key(부모 노드) <= key(자식 노드)


### Priority Queue (우선 순위 큐)
- 우선순위가 가장 높은 요소에 빠르게 접근해야 하는 경우에 Heap을 활용하여 구현할 수 있다
- 정렬 알고리즘: Heap Sort 알고리즘은 힙을 이용하여 정렬을 수행
- 작업 스케줄링: 힙을 사용하여 우선순위가 가장 높은 작업을 먼저 처리하는 스케줄링을 구현
- Heap은 우선순위를 관리하는 자료 구조로써, 최대/최소 값을 효율적으로 관리하고자 할 때 유용
# Graph

### Graph
- 노드(N, node)와 그 노드를 연결하는 간선(E, edge)을 하나로 모아 놓은 자료 구조
- 연결되어 있는 객체 간의 관계를 표현할 수 있는 자료 구조로 지도, 지하철 노선도의 최단 경로, 전기 회로의 소자들, 도로(교차점과 일방 통행길), 선수 과목 등에 이용된다
- 노드들 사이에 무방향/방향에서 양방향 경로를 가질 수 있어 2개 이상의 경로가 가능
- Tree와 다르게 루트 노드의 개념이 존재하지 않는다
- <details>
  	<summary>Graph 관련 용어</summary>
    <ul>
      <li>정점(vertex): 위치 (Node)</li>
      <li>간선(edge): 위치 간의 관계. 즉, 노드를 연결하는 선</li>
      <li>인접 정점(adjacent vertex): 간선에 의 해 직접 연결된 정점</li>
      <li>정점의 차수(degree): 무방향 그래프에서 하나의 정점에 인접한 정점의 수</li>
      <li>진입 차수(in-degree): 방향 그래프에서 외부에서 오는 간선의 수</li>
      <li>진출 차수(out-degree): 방향 그래픙에서 외부로 향하는 간선의 수</li>
      <li>경로 길이(path length): 경로를 구성하는 데 사용된 간선의 수</li>
      <li>단순 경로(simple path): 경로 중에서 반복되는 정점이 없는 경우</li>
      <li>사이클(cycle): 단순 경로의 시작 정점과 종료 정점이 동일한 경우</li>
    </ul>
  </deatils>
  

### Graph 종류
- Undirected Graph(무방향 그래프)
	- 무방향 그래프의 간선은 간선을 통해서 양 방향으로 갈 수 있다
	- 정점 A와 정점 B를 연결하는 간선은 (A, B)와 같이 정점의 쌍으로 표현
 	- (A, B)는 (B, A) 동일
    
- Directed Graph(방향 그래프)
	- 간선에 방향성이 존재하는 그래프
	- A -> B로만 갈 수 있는 간선은 <A, B>로 표시
	- <A, B>는 <B, A>는 다름
    
- Weighted Graph(가중치 그래프)
	- 간선에 비용이나 가중치가 할당된 그래프
	- ‘네트워크(Network)’ 라고도 한다.
    
- Connected Graph(연결 그래프)
	- 무방향 그래프에 있는 모든 정점쌍에 대해서 항상 경로가 존재하는 경우
	- Ex) 트리(Tree): 사이클을 가지지 않는 연결 그래프
    
- Disconnected Graph (비연결 그래프)
	- 무방향 그래프에서 특정 정점쌍 사이에 경로가 존재하지 않는 경우
    
- Complete Graph (완전 그래프)
	- 그래프에 속해 있는 모든 정점이 서로 연결되어 있는 그래프

### Graph 탐색 방법
- Breadth-First Search(너비 우선 탐색)
- Depth-First Search(깊이 우선 탐색) 
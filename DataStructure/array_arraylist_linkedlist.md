# Array, ArrayList, LinkedList

### Array
- 동일한 데이터 유형의 요소를 순차적으로 저장하는 자료 구조
- 크기가 고정되어 있으며, 한 번 생성된 후에는 크기를 변경할 수 없다
- 요소에 대한 빠른 접근이 가능하며 인덱스를 통해 직접 접근(Random Access)할 수 있다
- 데이터의 삽입 및 삭제가 비효율적이며, 크기가 작을 때 사용하기 적합

### ArrayList
- 크기를 동적으로 조정할 수 있는 배열 기반의 자료 구조
- 요소를 순차적으로 저장하며, 필요에 따라 크기를 자동으로 늘리거나 줄일 수 있다
- 데이터의 크기가 동적으로 변할 때 사용하기 적합하며, 다양한 기능과 메서드를 제공
- <details>
    <summary>ArrayList Method</summary>
  
  추가 / 삭제 
    <ul> 
        <li> add(element): ArrayList의 마지막에 요소를 추가</li>
        <li> add(index, element): 지정한 인덱스에 요소를 추가</li>
        <li> remove(index): 지정한 인덱스의 요소를 삭제</li>
      	<li> remove(element): 지정한 요소를 삭제</li>
    </ul>
  접근 / 검색
    <ul> 
        <li>get(index): 지정한 인덱스의 요소를 반환</li>
        <li>set(index, element): 지정한 인덱스의 요소를 새로운 요소로 대체</li>
        <li>contains(element): 지정한 요소가 ArrayList에 포함되어 있는지 확인</li>
      	<li>indexOf(element): 지정한 요소의 첫 번째 등장 인덱스를 반환</li>
      	<li>lastIndexOf(element): 지정한 요소의 마지막 등장 인덱스를 반환</li>
  </ul> 	
  그 외
    <ul> 
        <li>size(): ArrayList의 요소 개수를 반환</li>
      	<li>isEmpty(): ArrayList가 비어 있는지 확인</li>
      	<li>clear(): ArrayList의 모든 요소를 삭제</li>
      	<li>toArray(): ArrayList를 배열로 변환</li>
      	<li>addAll(collection): 다른 컬렉션의 모든 요소를 ArrayList에 추가</li>
      	<li>clone(): ArrayList의 얕은 복사본을 생성</li>
      	<li>iterator(): ArrayList를 반복하는 데 사용할 수 있는 Iterator 객체를 반환</li>
      <li>forEach(action): 모든 요소에 대해 지정한 동작을 수행</li>
    </ul>
</details>


### LinkedList
- 각 요소가 다음 요소를 가리키는 링크로 연결되어 있는 자료 구조
- 데이터의 삽입 및 삭제가 빠르며, 중간에 요소를 삽입하거나 삭제하는 작업이 효율적이다
- 요소에 순차적으로 접근하는데는 상대적으로 느리다
- 메모리 공간을 더 많이 사용하며, 특정 요소에 접근하기 위해 링크를 타고 가야하므로 처리 속도가 느릴 수 있다


### Array, ArrayList, LinkedList 비교
#### 공통점
- 모두 자료를 순차적으로 저장하는 자료구조

#### 차이점
- Array는 크기가 고정되어 있지만, ArrayList와 LinkedList는 동적으로 크기를 조정할 수 있다.
- Array와 ArrayList는 인덱스를 통해 요소에 직접 접근할 수 있지만, LinkedList는 순차적인 접근이 필요하다.
- Array는 데이터의 삽입 및 삭제가 비효율적이지만, ArrayList와 LinkedList는 삽입 및 삭제가 상대적으로 효율적이다.
- ArrayList와 LinkedList는 메모리 사용 및 처리 속도 측면에서 차이가 있다. ArrayList는 연속된 메모리를 사용하므로 접근 속도가 빠르지만, LinkedList는 링크를 타고 이동해야 하므로 상대적으로 느릴 수 있다.

# Database

### Anomaly 이상현상
#
  * 데이터베이스의 구조나 관계에 오류가 발생하여 정보를 정확하게 검색하거나 조작할 수 없는 상태
  * 데이터의 무결성과 일관성을 해치는 원인
  * 종류
    * Insertion Anomaly 삽입 이상 : 의도하지 않은 자료가 삽입되거나 필수적인 속성들이 모두 입력되지 않아 삽입이 제대로 이루어지지 않는 경우 발생하는 이상
    * Deletion Anomaly 삭제 이상 : 특정 레코드를 삭제하면 필요한 다른 레코드들도 함께 삭제되는 경우로 원하지 않는 정보 손실이 발생하는 이상
    * Update Anomaly 갱신 이상 : 데이터 수정시 일부만 변경되어 데이터가 불일치하는 모순, 또는 중복되는 튜플이 존재하게 되는 이상 현상
  * 예방
    * 정규화 과정을 통해 데이터를 올바르게 구조화
    * 제약 조건을 설정하여 데이터의 무결성을 유지
    * 트랜잭션을 적절하게 처리하여 데이터의 일관성을 유지

<br> 

### Normalization 정규화
#
  * 데이터베이스의 구조를 최적화하여 중복을 제거하고 데이터의 무결성을 유지하는 작업
  * 데이터베이스의 성능을 향상시키고 이상현상을 방지
  * 종류
    * 제 1 정규화 (1NF) : 모든 도메인이 원자값으로 이루어진 테이블을 생성하는 것을 목표로 각 속성은 하나의 값만 가지며, 중복된 데이터를 허용하지 않음
    * 제 2 정규화 (2NF) : 부분 함수 종속을 제거하여 테이블의 모든 열이 기본 키에 완전히 종속되도록 만드는 것을 목표로 기본 키가 아닌 속성들은 기본 키에 대해 완전히 종속 됨
    * 제 3 정규화 (3NF) : 이행적 함수 종속을 제거하여 테이블의 모든 열이 기본 키에 대해서만 종속되도록 만드는 것을 목표로 기본 키가 아닌 속성들 간에도 종속 관계가 없어야 함

<br>

> **완전 함수 종속** <br>
> 기본 키의 모든 속성들로만 다른 속성들의 값을 유일하게 결정할 수 있는 상태
> 
>  **부분 함수 종속** <br>
> 한 속성이 기본 키의 일부만을 결정하는 관계
>
> [주문] 테이블
> |주문 번호|고객 번호|고객 이름|주문 날짜|
> |:---:|:---:|:---:|:---:|
> |1|101|Lee|2023-07-20|
> |2|102|Park|2023-07-30|
> |3|103|Kim|2023-07-31|
> |
>
> [주문]테이블
> |주문 번호|고객 번호|주문 날짜|
> |:---:|:---:|:---:|
> |1|101|2023-07-20|
> |2|102|2023-07-30|
> |3|103|2023-07-31|
> |
>
> [고객 ]테이블
> |고객 번호|고객 이름|
> |:---:|:---:|
> |101|Lee|
> |102|Park|
> |103|Kim|
> |

<br>

> **이행적 함수 종속**<br>
> 데이터베이스 테이블에서 한 속성이 다른 속성을 통해 종속되는 관계<br>
> 데이터의 중복과 이상현상이 발생 할 수 있음<br>
> A -> B, B -> C 일 때 A -> C 성립

<br>

### Denomarlization 역정규화
#
  * 정규화는 이상현상을 최소화하기 위해 테이블을 쪼개는 작업이지만 지나친 정규화는 쿼리를 복잡하게 만들고 성능을 저하될 수 있으므로 이를 방지하여 전반적인 성능을 향상시키기 위함
  * 테이블이 단순해지고 관리 효율성이 증가되나 데이터의 일관성이나 무결성이 보장지 않을 수 있음
  * 역정규화를 사용할 때는 성능 향상과 데이터 일관성 사이에서 적절한 균형을 찾아야함

<br>

### Transaction 트랜잭션
#
  * 데이터베이스에서 하나의 논리적 기능을 수행하기 위한 작업의 단위
  * ACID 특징
    * Atomicity 원자성 : 모든 작업이 수행 되거나 문제가 발생한다면 어떠한 작업 내용도 수행되지 않음을 보장, "All or Nothing"
    * Consistency 일관성 :  트랜잭션 실행 전 후로 일관성 보장
    * Isolation 고립성  : 각각의 트랜잭션은 독립적으로 수행
    * Durability 지속성 : 트랜잭션 결과를 영구적으로 반영
  * 격리 수준
    * SERIALIZABLE : 한 트랜잭션이 COMMIT 될까지 다른 트랜잭션은 CRUD 불가
    * REPEATABLE_READ : 조회중인 데이터를 다른 트랜잭션에서  UPDATE 불가
    * READ_COMMITTED : COMMIT 된 데이터만 조회 가능
    * READ_UNCOMMITTED : 다른 트랜잭션에서 COMMIT 되지 않은 데이터도 접근 가능
  * 상태 <img alt="status_transaction" src="https://blog.kakaocdn.net/dn/bbYMDH/btrbOsjZF2N/le9kHXH4DkZIb67wbfoFw0/img.png">
    * Active: 트랜잭션이 작업을 시작하여 실행 중인 상태
    * Failed: 트랜잭션에 오류가 발생하여 실행이 중단된 상태
    * Aborted: 트랜잭션이 비정상적으로 종료되어 Rollback 연산을 수행한 상태
    * Partially Committed: 최종 결과를 데이터베이스에 아직 반영하지 않은 상태
    * Committed: 트랜잭션이 성공적으로 종료되어 commit 연산을 실행한 후의 상태
  * 연산
    * Commit: 트랜잭션이 성공적으로 처리되었다고 확정하는 명령어로 변경된 내용을 영구적으로 저장
    * Rollback: 트랜잭션으로 처리한 과정을 일어나기 전으로 되돌리는 명령어
    * Commit과 Rollback을 통해 데이터의 무결성을 보장
  * 주의사항
    * 데이터베이스 Connection 개수가 제한적이기 때문에 트랜잭션 범위를 최소화 해야 함
    * Connection을 소유하는 시간이 길어 질 수록 사용가능한 Connection수가 줄어 들어 대기시간이 길어 질 수 있음

<br>


### DBLock
#
  * 동시에 데이터베이스에 접근할 때 데이터의 일관성과 무결성을 유지하기 위해 사용되는 동시성 제어 기술
  * Shared Lock / Read Lock 공유락
    * 다른 트랜잭션이 읽기만 가능하도록 허용하는 락
    * 여러 트랜잭션들이 같은 데이터에 공유 락을 획득할 수 있으며, 읽기 작업 중에는 다른 트랜잭션이 해당 데이터에 대한 수정 락을 얻는 것을 막음
    * Select문에 의해 실행
  * Exclusive Lock / Write Lcok 배타락
    * 다른 트랜잭션들이 읽기나 쓰기 작업을 할 수 없도록 하고, 해당 데이터를 독점적으로 사용하도록 허용하는 락
    * 특정 트랜잭션이 수정 락을 획득한 경우, 다른 트랜잭션들은 해당 데이터에 접근할 수 없음
    * INSERT, UPDATE, DELETE 문에 의해 실행
  * 트랜잭션의 실행 계획에 따라 자동으로 관리되기도 하며, 개발자가 명시적으로 락을 사용하기도 함
  * 락을 지나치게 많이 사용하면 동시성이 저하되거나 데드락(Deadlock)과 같은 문제가 발생할 수 있음

<br>

### Blocking 블로킹
#
  * Lock 간의 경합(Race Condition)이 발생하여 특정 Transaction이 작업을 진행하지 못하고 멈춰선 상태
  * 공유락끼리는 블로킹이 발생하지 않지만, 배타락은 블로킹을 발생

<br>

### DeadLock 교착상태 
#
  * 트랜젝션 간 각각 가지고 있는 리소스의 Lock을 획득하려고 할 때 발생으로 자원이 사용가능 해 질때 까지 무한 대기인 상태
  * 해결 방안
    * Dead Lock이 감지되면 둘 중 하나의 트랜잭션을 강제 종료한다.
    * 실제로, Oracle 에서는 데드락이 감지되면 한쪽 Transaction을 강제로 풀어버린다. 이렇게 되면 하나의 트랜잭션A의 마지막 실행 내용에 오류가 발생되고 커밋이 발생되도록 유지한다. 또다른 트랜잭션 B는 아직 대기중이며, 트랜잭션 A의 커밋을 기다린다.
    * Dead Lock 방지를 위해 접근 순서를 동일하게 하는 것이 중요하다. 접근 순서 규칙을 정할 필요가 있다.

<br>

> **Blocking vs Dead Lock**<br><br>
> 블로킹한 트랜잭션이 끝나면 블로킹은 언젠가 반드시 사라진다. 하지만 데드락은 서로가 서로에게 블로킹을 걸었기 때문에 상대 트랜잭션이 끝나기만을 서로 기다리다가 계속해서 끝나지 않는다.

<br>

### Join
#
  * 두 개 이상의 테이블을 연결하여 하나의 결과 집합을 생성하는 작업
  * 데이터베이스에서 데이터들을 효율적으로 검색하기 위해 사용되며, 특히 다양한 테이블에 분산되어 있는 데이터들을 필요에 맞게 결합할 때 유용
  * 종류
    * Inner Join 내부 조인 : 양쪽 테이블의 두행이 모두 일치하는 행이 있는 데이터만 추출
    * [Left/Outer/Full] Outer Join : 한쪽에는 데이터가 있고 한쪽에는 없는 경우, 데이터가 있는 쪽의 내용을 전부 추출

<br>

> **WHERE와 JOIN에서 ON의 차이**
>
> **WHERE** : JOIN 결과를 WHERE 조건절로 필터링이 이뤄짐<br>
> **ON** : JOIN 대상이 ON 조건으로 필터링 됨

<br>

### DELETE vs TRUNCATE vs DROP
#
  * DELETE 
    * 조건에 해당하는 데이터를 삭제
    * Rollback 가능 
  * TRUNCATE
    * 테이블 구조를 제외한 모든 데이터를 삭제
    * 테이블의 데이터를 전부 삭제하고 사용하고 있던 공간을 반납
    * Rollback 불가능
  * DROP
    * 테이블 자체를 완전히 삭제
    * Rollback 불가능

<br>

### JDBC vs ODBC
#
  * JDBC와 ODBC는 데이터베이스와 애플리케이션 간에 상호작용하기 위한 데이터베이스 접속 기술
  * JDBC (Java Database Connectivity)
    * JDBC는 자바 애플리케이션에서 데이터베이스와 상호작용하기 위한 자바 API 
    * Java에서 데이터베이스 연결과 쿼리 수행
  * ODBC (Open Database Connectivity)
    * ODBC는 마이크로소프트가 개발한 표준 데이터베이스 API
    * 다양한 프로그래밍 언어와 데이터베이스 관리 시스템 간의 상호운용성을 제공

<br>

### Optimizer 옵티마이저
#
  * 데이터베이스 관리 시스템(DBMS)에서 쿼리를 처리할 때, 가장 효율적인 실행 계획을 결정하는 역할을 담당하는 컴포넌트
  * 쿼리를 처리하는 방법 중에서 가장 최적의 방법을 선택하여 데이터베이스의 성능을 최적화
  * 데이터베이스 쿼리가 복잡하고 대용량 데이터를 다룰 때, 옵티마이저의 성능은 데이터베이스 시스템 전체의 성능에 큰 영향
  * 기능
    * 실행 계획 생성 : 데이터베이스 시스템의 요구 사항에 따라 다르며, 쿼리의 조건과 인덱스, 테이블 크기, 통계 정보 등을 고려
    * 비용 산정 : 실행 계획에 대해 예상 비용을 산정하여 가장 효율적인 실행 계획을 선택
    * 실행 계획 선택 : 쿼리를 가장 빠르고 효율적으로 실행할 수 있는 방법을 결정
    * 통계 정보 관리 : 데이터베이스의 통계 정보를 관리, 통계 정보를 기반으로 옵티마이저는 실행 계획을 결정
    * 동적 계획 조정 : 옵티마이저는 실행 시간에 동적으로 계획을 조정하여 최적의 성능을 유지
  * 종류
    * 규칙 기반 옵티마이저 : 미리 정의된 규칙에 따라 실행 계획을 결정하는 방식
    * 비용 기반 옵티마이저 : 비용 산정을 통해 실행 계획을 선택하는 방식으로 가장 널리 사용
    * 휴리스틱 옵티마이저: 경험에 의존하여 실행 계획을 결정하는 방식
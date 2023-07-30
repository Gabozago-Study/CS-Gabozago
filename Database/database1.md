# Database

### DB를 사용하는 이유
#
* 확장성이 좋음 (파일 시스템은 OS 종속적)
* 중복 최소화, 보안성
* 원자성, 일관성 유지를 위한 동시성 제어, 백업 및 회복 등의 여러 데이터 관리 기능을 통해 데이터를 편하게 관리할 수 있음

<br/>

### DBMS (DataBase Management System)
#
* 데이터베이스를 관리하고 운영하는 소프트웨어
* 특징
    * 응용 프로그램들이 데이터베이스에 접근할 수 있는 인터페이스 제공
    * 복구와 보안 기능을 통해 DB 조작을 편리하게 함
    * 구조적 질의 언어 (Structure Query Language)를 통해 삽입, 삭제, 수정, 조회 등을 수행
    * 대부분의 DBMS는 테이블로 이뤄진 RDBMS(Relational DBMS) 형태로 사용
* 기능
    * 정의 : 테이블, 속성 등 DB 구조 정의
    * 조작 : 삽입, 수정, 삭제, 검색 등 DB 연산 처리
    * 제어 : 데이터 무결성, 일관성, 접근 권한, 동시성 제어    

<br/>

### SQL
#
* DDL(Data Definition Language 데이터 정의어)
    * 데이터베이스 구조를 정의, 수정, 삭제하는 언어
    * CREATE, DROP, ALTER
* DML(Data Manipulation Language 데이터 조작어)
    * 조회, 삽입, 수정, 삭제와 같은 데이터 관리를 위한 언어
    * SELECT, INSERT, UPDATE, DELETE 
* DCL(Data Control Language 데이터 제어어)
    * 데이터 무결성 및 접근 권한을 다루기 위한 언어
    * COMMIT, ROLLBACK, GRANT, REVOKE

<br/>

### RDBMS VS NoSQL
#
* RDBMS (Relational Database Management System)
    * 데이터를 2차원 테이블 형태로 표현
    * 관계를 맺고 모여있는 테이블들의 집합체
    * 테이블 간의 관계에서 서로의 칼럼을 기준으로 Join이 가능
    * 정해진 스키마에 따라 데이터를 저장하기 때문에 명확한 데이터 구조 보장
    * 시스템이 커질수록 Join문이 많은 복잡한 쿼리가 필요하여 성능 저하
    * 예: MySQL, Oracle 등

* NoSQL (Not Only SQL)
    * Key-Value, Document, Big Table, Graph 방식으로 데이터를 관리
        * Key-value 방식(Redis): 키를 고유한 식별자로 사용하여 키-값 쌍으로 데이터를 저장
        * Document 방식(MongoDB): XML이나 JSON, YAML 같은 데이터 타입(document)을 이용해서 레코드를 저장
        * Big Table 방식(Hbase, Casandra): key-value와 데이터 저장 방식은 동일하며, 추가적으로 key 정렬 기능이 제공됨
        * Graph 방식(Sones, Allegro Graph): 데이터를 노드로 표현하고, 노드 사이의 관계를 화살표로 표현
    * 비 관계형 데이터베이스
        * 관계가 없기 때문에 Join이 불가능하고 트랜젝션을 지원하지 않음
    * 스키마가 없으므로 자유로운 데이터 구조를 갖음
    * 데이터를 여러 대의 서버에 분산해 저장하여 특정 서버에 장애가 발생했을 때도 데이터 유실이나 서비스 중지가 없도록 함
    * 자주 변경되지 않는 데이터를 저장하기 유리하며 읽기, 쓰기가 빠름
    * 데이터 중복이 발생할 수 있으므로 데이터 일관성, 무결성 관리에 유의
    * 인덱스 구조를 메모리에 저장하기 때문에 많은 인덱스를 사용하려면 충분한 메모리가 필요
    * 예: Redis, MongoDB 등

* 정리
    * 데이터가 자주 변경이 이루어지는 시스템에서는 RDBMS를,
    * 막대한 데이터로 인한 DB Scale-out 필요 시, NoSQL을 사용

<br/>

### Redis (Remote Dictionary System)
#
* NoSQL 방식을 사용하는 인메모리 데이터베이스
* Key-Value 형식으로 데이터를 저장
* 주로 어플리케이션 캐시나 빠른 응답 속도를 가진 데이터베이스로 사용
* Redis의 데이터 휘발을 막기 위한 방법
    * Snapshot 기능을 통한 디스크 백업
    * AOF(Append Only File) 기능을 통한 명령 쿼리 저장
        * 모든 write/update 연산 자체를 모두 log 파일로 기록
        * 서버가 실행되면 순차적으로 연산을 재실행하여 데이터를 복구

<br/>

### ERD (Entity Relationship Diagram)
#
* 데이터베이스를 구축할 때 가장 기초적인 뼈대로 릴레이션 간의 관계들을 정의
* 시스템의 요구사항을 기반으로 작성되며 ERD를 기반으로 데이터베이스를 구축
* 관계형 구조로 표현할 수 있는 데이터를 구성하는데 유용하지만 비정형 데이터를 충분히 표현할 수 없음
 
<br/>

### KEY
#
* 테이블 간의 관계를 명확하게 하고 검색, 정렬 시 튜플을 구분하는 기준이 되는 속성
* 종류
    * 슈퍼키 (Super Key) : 유일성을 만족하지만 최소성은 만족하지 못하는 키
    * 후보키 (Candidate Key) : 유일성과 최소성을 만족하는 키
        * 기본키 (Primary Key) : 후보키에서 특별히 선정된 키로 중복된 값과 Null값을 가질 수 없음
        * 대체키 (Alternate key) : 유일성과 최소성을 만족하지만 기본키로 선택되지 못한 키
    * 외래키 (Foreign Key) : 다른 테이블의 기본키를 참조하는 값으로 관계 식별에 사용되는 키
* 특징
    * 유일성: 키로 튜플을 유일하게 식별할 수 있음
    * 최소성: 튜플을 구분하는데 필요한 최소한의 속성들로만 구성

<br/>

### 관계
#
* 여러 테이블 간의 논리적 연결을 의미하며 주로 외래키(foreign key)를 통해 위 관계를 명시
* 종류
    * 1:1 관계 (일대일)
        * 하나의 레코드가 다른 테이블의 레코드 한 개와 연결된 경우
    * 1:N 관계 (일대다)
        * 하나의 레코드가 다른 테이블의 서로 다른 여러 개의 레코드와 연결된 경우
        * 가장 많이 사용되는 관계
    * N:M 관계 (다대다)
        * 두 개의 테이블이 N:1 관계와 1:M 관계가 합쳐진 경우

<br/>
 
### 데이터베이스 무결성
#
* 데이터의 정확성, 일관성 등을 유지하는 것
* 개체 무결성 (Entity Integrity)
    * 기본키(Primary Key)는 중복된 값을 가질 수 없으며 Null값이 올 수 없음
* 참조 무결성 (Referential Integrity)
    * 외래키(Foreign Key)는 상위 테이블에 반드시 존재하는 값이거나 Null이어야 함
    * 참조 관계에 있는 두 테이블의 데이터 일관성 보장
* 도메인 무결성 (Domain Integrity)
    * 특정 속성의 값이 그 속성이 정의된 도메인에 속한 값이어야 함
    * 데이터의 무결성을 보장
* 이 외에 고유 무결성, NULL 무결성, 키 무결성 등이 있음
    * 고유 무결성: 특정 속성에 대해 고유한 값을 가지도록 조건이 주어진 경우, 그 속성값은 모두 달라야 하는 제약조건
    * NULL 무결성: 특정 속성값에 NULL 이 올 수 없다는 조건이 주어진 경우, 그 속성값은 NULL 값이 올 수 없다는 제약조건
    * 키 무결성: 한 릴레이션(테이블)에는 최소한 하나의 키가 존재해야 한다는 제약 조건

<br/>

### Index
#
<img alt="index" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcQi8RP%2Fbtq8BkRrRfb%2Fa5C0jH5pfSA2KKz7C9fB7k%2Fimg.png">

* 데이터에 대한 검색 성능의 속도를 높여주는 자료 구조 
* 별도의 메모리 공간에 Key-Value형태로 데이터와 데이터의 물리적인 주소를 함께 저장
* 특징
    * 항상 정렬된 상태를 유지하기 때문에 원하는 값을 빠르게 검색할 수 있음
    * 데이터 삽입, 삭제, 수정 시 2개의 컬럼을 수정해서 재정렬을 해야하므로 속도가 느림
* 사용 조건
    * 추가적인 메모리 공간을 필요하므로 자주 사용되는 컬럼에 Index를 설정하는 것이 좋음
    * 데이터가 많거나 Join이 많은 경우에 적합
        *  Index가 없을 경우, Join 작업 시 모든 테이블 레코드를 스캔하여 일치하는 데이터를 찾으므로 이 때 Index를 사용하면 작업에 필요한 값들을 더 빠르게 찾을 수 있음
    * 데이터의 삽입/삭제/갱신이 잦은 경우에서는 불필요

<br/>

### Index 자료 구조
#

<img alt="b-tree" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FBLi5L%2FbtrdInhxyVP%2Febff3uYkmyoEty5lULR8kK%2Fimg.png">

* B-Tree
    * 탐색 성능을 높이기 위해 균형 있게 높이를 유지하는 Balanced Tree의 일종
        * 편향된 트리에서 leaf node까지 탐색한다면 모든 node를 방문하기 때문에 O(N)의 시간이 걸리게 되는 단점은 보완
        * 최상의 경우 특정 key를 root node에서 찾을 수 있음
    * Full scan 시, 모든 노드 탐색

<img alt="b+tree" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbAARBC%2FbtrdDydoUp7%2F9h4KOXBRyDNKpKDAe2ugq0%2Fimg.png">

* B+Tree
    * 오직 leaf node에만 데이터를 저장하고 leaf node가 아닌 node에는 자식 포인터만 저장
        * 하나의 node에 더 많은 포인터를 가질 수 있기 때문에 트리의 높이가 더 낮아지므로 검색 속도를 높일 수 있음
        * 반드시 특정 key에 접근하기 위해서 leaf node까지 가야함
    * leaf node끼리는 Linked list로 연결
        * Full scan 시, 리프 노드에서만 탐색

* 해시 테이블
    * key와 value를 한 쌍으로 데이터를 저장하는 자료구조
    * 평균적으로 O(1)의 매우 빠른 시간만에 원하는 데이터를 탐색할 수 있음
    * 데이터가 정렬되지 않은 상태로 등호 연산에 최적화되어있어, 부등호 연산이 많은 DB에서는 잘 사용되지 않음

<br/>

### Partitioning
#
* 큰 테이블이나 인덱스를 작은 파티션(Partition) 단위로 나누어 관리하는 기법
* 장점
    * Full Scan에서 데이터 접근의 범위를 줄여 성능을 향상시킬 수 있음
    * 큰 테이블들을 제거하여 관리를 쉽게 할 수 있음
    * 파티션 별로 독립적으로 백업하고 복구할 수 있음
* 단점
    * Join 비용
    * 테이블과 인덱스를 별도로 파티셔닝 할 수 없음

<br/>

### View
#
* 데이터를 제한적으로 보여주기 위한 가상 테이블
* 장점
    * view에 나타나지 않은 데이터를 간편히 보호할 수 있음
    * 필요한 데이터만 뷰로 정의해서 처리할 수 있기 때문에 관리가 용이하고 명령문이 간단해짐
* 단점
    * Alter를 사용하여 뷰의 정의를 변경할 수 없음
    * 독립적인 인덱스를 가질 수 없음
  
<br/>

### Trigger
#
* 특정 테이블에서 INSERT, DELETE, UPDATE 같은 DML문이 수행되었을 때, <b>데이터베이스에서 자동으로 동작</b>하도록 작성된 프로그램
* 장점
    * 데이터 무결성의 강화 (참조 무결성)
    * 업무처리 자동화
* 단점
    * 트리거를 과도하게 사용한다면 복잡한 상호 의존성이 생김
* 사용 시 주의 사항
    * 트리거에서 같은 테이블의 데이터를 변경하는 DML 문을 실행하는 경우 무한 루프에 빠질 수 있음
        * 예: Insert 이벤트에 대한 Trigger로 Insert 이벤트가 실행 된다면 무한 루프에 빠지게 됨

<br/>

### SQL Injection
#
* 악의적인 의도로 SQL 구문을 삽입하여, 데이터베이스를 비정상적으로 조작하는 코드 인젝션 공격 기법
* 해결 방안
    * 저장 프로시저 사용하여 Query에 미리 형식을 지정하여 지정된 형식의 데이터가 아니면 Query가 실행되지 않도록 함

<br/>

### 기타 용어
#
Schema: 데이터베이스에 저장되는 데이터 구조와 제약조건을 정하는 것 <br/>
Table: 행과 열로 구성된 데이터 집합 <br/>
Sequence: 기본키가 유일한 값을 갖도록 순번을 자동 생성해주는 데이터베이스 객체 <br/>
Stored Procedure: 일련의 쿼리를 마치 하나의 함수처럼 실행하기 위한 쿼리의 집합 <br/>

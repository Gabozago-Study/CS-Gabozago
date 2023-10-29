# Spring

### Spring, Spring MVC, Spring Boot의 차이
Spring
* 자바의 오픈 소스 애플리케이션 프레임워크
* 객체를 관리할 수 있는 컨테이너 제공
* IOC, DI, AOP를 지원
  
Spring MVC
* 웹 애플리케이션 개발을 위한 기능을 제공
* Model: 비지니스 로직를 처리, DB와 상호작용하는 모듈
* View: Client에게 보여지는 화면을 반환하는 모듈
* Controller: 모델과 뷰 사이의 정보 교환, Client 요청이 들어왔을 때, 어떤 로직을 실행할 것인지 제어하는 모듈

Spring Boot
* Spring 기반의 애플리케이션을 간편하게 설정할 수 있는 도구
* 내장 서버: Embeded Tomcat이 포함되어 있어 Tomcat을 따로 설치/관리할 필요가 없음. 하지만 많은 용량을 처리할 수 없으므로 테스트 용도가 아니라면 꼭 서버를 설치해야함
* Spring을 보다 편리하게 사용할 수 있도록 하기 위한 도구 기존의 많은 설정이 자동화 (spring boot starter dependency), 버전 관리도 자동으로 됨

### Bean이란
* Spring IoC 컨테이너가 관리하는 자바 객체, 필요할 때 컨테이너에서 가져와서 사용
* 스프링 컨테이너에 의해 생명주기 관리
    * 객체 생성 -> 의존 설정 -> 초기화 -> 사용 -> 소멸
  
### @Bean 과 @Component의 차이
@Bean
* 메소드 레벨에서 선언
* 반환되는 객체(인스턴스)를 개발자가 수동으로 등록

@Component
* 클래스 레벨에서 선언
* 스프링이 런타임시에 컴포넌트스캔을 하여 자동으로 빈을 등록
* 애플리케이션이 실행되면 비어있는 스프링 컨테이너가 생성 -> 스프링 설정 파일이나 어노테이션 기반으로 컨테이너에 스프링 빈이 등록 -> 의존관계가 주입

### Container란
* 인스턴스의 생명주기를 관리
* 코드를 참조하여 객체의 생성과 소멸을 컨트롤

### IOC(Inversion of Control, 제어의 역전)란
* 제어권이 개발자에게 있지 않고, 프레임워크에 있어서 필요에 따라서 사용자의 코드를 호출, 이러한 현상을 "제어의 역전"이라고 표현
* Spring 프레임워크에서 지원하는 Ioc Container는 일반 POJO의 생명주기를 관리하며, 생성된 인스턴스들에게 추가적인 기능들을 제공


### DI
Dependency Injection, 의존성 주입
* 객체 간의 의존 관계를 미리 설정해 두면 스프링 컨테이너가 의존 관계를 자동으로 연결
* 의존하는 객체를 직접 생성하거나 검색해서 가져올 필요가 없어 결합도가 낮아짐
* 클래스를 재사용 할 가능성을 높이고, 다른 클래스와 독립적으로 클래스를 테스트 가능
* 의존성 주입 방법
  * 1. 생성자 주입(생성자에 @Autowired 추가) (권장!)
    * 순환 참조 방지: 다른 주입 방식과 달리 스프링 애플리케이션 로딩시점에서 예외가 발생하여 실제 코드가 호출되기 전 오류를 확인할 수 있음
    * 불변성(Immutability): final로 참조형 변수는 반드시 선언과 함께 초기화가 되어야 하므로 누군가 해당 객체값을 임의로 변경할 수 없음
  * 2. 필드 주입(필드에 @Autowired 추가)
  * 3. setter 주입(setter에 @Autowired 추가)


### AOP (Asper-Oriented Programming 관점지향 프로그래밍) 
* 핵심 기능 외 부수 기능들을 분리 구현하므로써 모듈성을 증가시키는 방법
* 메서드 안의 주기능과 보조 기능을 분리한 후 선택적으로 메서드에 적용해서 사용
* 트랜잭션이나 로깅, 보안과 같이 공통적으로 사용하는 기능들을 분리하여 관리
* OOP: Business Logic의 모듈화, AOP: 기능의 모듈화



### POJO(Plain Old Java Object)
* 프레임워크 인터페이스나 클래스를 구현하거나 확장하지 않는 단순한 클래스
* Java에서 제공하는 API 외에 종속되지 않음
* 코드의 간결함
* 비즈니스 로직과 특정 환경이 분리되므로 단순함
* 자동화 테스트에 유리 
* 단순 getter, setter만으로 구성되어 있으며 new를 통해서 생성 가능한 형태

### Entity, DAO, DTO, VO의 차이
Entity
* 실제 DataBase의 테이블과 1 : 1로 매핑되는 클래스
* DB의 테이블내에 존재하는 컬럼만을 속성(필드)으로 가져야 함
* 상속을 받거나 구현체여서는 안됨

DAO(Data Access Object)
* DB의 데이터를 조회하거나 조작하는 기능을 전담하도록 만든 객체를 말한다.
* DB에 접근을 하기위한 로직과 비즈니스 로직을 분리하기 위해서 사용 한다.

DTO(Data Transfer Object)
* 계층간 데이터 교환을 위한 데이터 교환을 위한 객체(Java Beans)를 말한다.
여기서 말하는 계층은 Controller, View, Business Layer, Persistent Layer 이다.
* 일반적인 DTO는 로직을 갖고 있지 않는 순수한 데이터 객체이며, 속성과 그 속성에 접근하기 위한 getter, setter 메소드만 가진 클래스이다.
  
VO(Value Object)
* 변하지 않는 데이터 객체, 오직 read만 가능하며 getter만 사용

### Annotation
* Java 소스 코드에 추가하여 사용할 수 있는 메타데이터의 일종으로 클래스와 메서드에 추가하여 다양한 기능을 부여하는 역할
* Annotation의 사용은 코드의 생산성을 증가시키고 코드량을 감소시키며 유지보수에 용이
* @RequestBody, @RequestParam, @ModelAttribute, @Bean, @Component ...

### Servlet과 DispatcherServlet
Servlet
* 클라이언트의 요청을 처리해 결과 반환, 웹 페이지를 동적으로 생성하기 위한 서버측 프로그램
* Spring MVC에서 Controller 역할 수행

DispatcherServlet
* 서버로 들어오는 요청을 처리하는 Front Controller
* 웹 요청의 진입점, 요청을 처리하여 결과를 응답

### ORM (Object Relational Mapping)
* 관계형 DB를 OOP 언어로 변환하는 기술
* 객체 클래스를 RDB 테이블에 자동으로 연결하는 것 -> SQL 없이 간접적으로 DB 조작 가능
* 비지니스 로직에 집중할 수 있음, DBMS 종속성 하락

### JPA Fetch 종류
* 즉시 로딩: 엔티티를 조회할 때, 연관된 엔티티도 함께 DB를 조회
* 지연 로딩: 엔티티를 조회할 때, 연관된 엔티티는 조회하지 않고 프록시 객체로 넣어두었다가 엔티티가 실제로 사용될 때 조회
> 프록시: 실제 엔티티 대신에 사용되는 객체, 원본 엔티티를 상속받은 객체

### PSA(Portable Service Abstraction)
* 일관된 서비스 추상화
* 작업 환경이나 기술이 변하더라도 일관된 방식의 접근 방식을 제공하여 의존성을 크게 고려하지 않아도 되는 구조
* 예시
    <img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FqBlwL%2FbtrpGzxt8xd%2FnXY5EU8z7Y4Q7hH4SVhZU1%2Fimg.png" alt="psa" width="100%">
* @Transactional: JDBC에 특화된 DatasourceTransactionManager, JPA에 특화되어 Entity Manager를 사용하는 JPATransactionManager를 각각 구현하는 것이 아니라, 최상위 추상화 인터페이스인 PlatformTransactionManager를 만들고 각각의 TransactionManager가 구현하도록 만들어서 DI로 주입받아 사용하도록 만들어짐

# Spring

### POJO (Plain Old Java Object) 설명
#
다른 클래스나 인터페이스를 상속하지 않고 getter, setter와 같이 기본적인 기능만 가진 자바 객체를 의미합니다.

<br>

### IoC(Inversion of Control, 제어의 역전) 설명
#
인스턴스 생명주기 관리를 개발자가 아닌 Spring 컨테이너가 대신하는 것을 의미합니다.

<br>

### Spring Container 설명
#
Spring Bean의 생명주기를 관리합니다.

<br>

### Spring Bean의 생명주기에 대한 설명
#
애플리케이션 실행 → 스프링 IoC 컨테이너 생성 → 설정 파일이나 어노테이션 기반으로 컨테이너에 스프링 빈 등록 → 의존관계 주입 → 초기화 콜백 메소드 호출 → 사용 → 소멸 전 콜백 메소드 호출 → 스프링 종료

<br>

### Spring Bean 등록 방법
#
class에 @Component를 선언하여 스프링이 실행될 때 컴포넌트 스캔을 통해 자동으로 빈을 등록할 수 있습니다.
또한 @Configuration이 선언된 클래스 내부에서 method에 @Bean을 선언하여 해당 메서드가 반환하는 객체를 빈으로 등록할 수 있습니다.

<br>

### DI(Dependency Injection, 의존성 주입)의 종류
#
생성자를 통한 주입, setter를 통한 주입, 필드를 통한 주입방법이 있습니다.
생성자를 사용할 경우, 의존성 주입을 강제할 수 있으며(NullPointerException 방지) 순환참조에 대한 오류를 미연에 방지할 수 있는 장점이 있습니다.

<br>

### AOP(Aspect Oriented Programming, 관점 지향 프로그래밍) 설명
#
애플리케이션 전체에 걸쳐 사용되는 부가 기능을 모듈화하여 재사용할 수 있도록 프로그래밍하는 것입니다. OOP는 비즈니스 로직의 모듈화, AOP는 기능의 모듈화라는 점에 있어 차이가 있습니다.

<br>

### PSA(Portable Service Abstraction, 일관된 서비스 추상화) 설명
#
작업 환경이 변하더라도 일관된 접근 방식을 제공하여 의존성을 크게 고려하지 않아도 되는 구조를 의미합니다.
이에 대한 예시로 Spring에서 DB에 접근할 때, JDBC와 JPA 모두 @Transactional을 사용하여 transaction을 관리할 수 있습니다.

<br>

### MVC 패턴이란
#
각 계층간의 기능을 구분하는데 중점을 둔 디자인 패턴으로, 로직을 분리함으로써 유지보수를 독립적으로 수행할 수 있습니다.
Model에서 데이터 관리 및 비즈니스 로직을 처리하며, View에서는 Client에게 보여지는 화면을 반환합니다. Controller는 사용자의 요청을 처리하고 Model과 View를 중개합니다.

<br>

### Servlet 설명
#
MVC 패턴에서 클라이언트의 요청을 처리해 결과 반환하는 controller 역할을 하며, 웹 페이지를 동적으로 생성하기 위한 서버측 프로그램입니다.
추가로 Dispatch Servlet은 서블릿 컨테이너의 가장 앞단에서 HTTP 프로토콜로 들어오는 모든 요청을 먼저 받아 적합한 컨트롤러에 위임해주는 컨트롤러입니다.

<br>

### Entity, DTO, VO, BO, DAO 차이
#
Entity는 실제 DB와 1:1로 매핑되는 클래스입니다.
Entity 클래스는 다른 클래스에 영향을 미칠 수 있으므로, View와 통신하며 자주 변경될 수 있는 데이터의 경우에는 DTO 클래스로 따로 분리해야 합니다.
DTO(Data Transfer Object)는 각 계층간의 데이터 교환을 위해 사용하는 데이터 객체입니다.
VO(Value Object)는 조회용(Read Only) 데이터를 저장하는 객체입니다.

DAO(Data Access Object)는 DB 데이터에 접근하여 조작하거나 조회하기 위한 객체입니다.
BO(Business Object)는 여러 DAO를 활용해 비즈니스 로직을 처리하는 객체입니다.

<br>

### Spring Boot와 차이
#
SpringBoot는 spring-boot-starter dependency를 통해 환경설정 및 버전관리를 간편히 할 수 있습니다.
내장 tomcat이 제공되어 따로 설치/관리할 필요가 없습니다.

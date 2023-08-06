# Design Pattern 2

### 객체지향 설계 원칙(SOLID)
 #
* SRP (Single Responsibility Principle) 단일 책임 원칙
     * 하나의 클래스는 하나의 책임만 가져야한다는 원칙
     * SRP를 잘 따르면 응집도(cohesion)는 높이고 결합도(coupling)은 낮출 수 있음
       * 응집도 : 모듈 내부의 기능적인 응집 정도
       * 결합도 : 모듈과 모듈간의 상호 결합 정도
 * OCP (Open Closed Principle) 개방 폐쇄 원칙
     * 요구사항의 변경이 발생하더라도, 기존 구성요소는 수정이 일어나지 말아야하며 쉽게 확장이 가능하여 재사용할 수 있어야 한다는 원칙
     * 추상화(Abstraction)와 다형성(Polymorphism)을 통해 실현할 수 있음
 * LSP (Liskov Substitution Principle) 리스코프 치환 원칙
     * 상속 관계에 있는 클래스들이 서로를 대체할 수 있어야 함
     * 부모 클래스의 인스턴스를 자식 클래스의 인스턴스로 대체해도 프로그램의 정확성을 보장해야 한다는 원칙
     * 다형성을 지원하기 위한 원칙
 * ISP (Interface Segregation Principle) 인터페이스 분리 원칙
     * 자신이 사용하지 않는 인터페이스는 구현하지 말아야 한다는 원칙
     * 인터페이스의 단일 책임을 강조
 * DIP (Dependency Inversion Principle) 의존 역전 원칙
     * 구체적인 구현 클래스에 의존하지 말고, 추상적인 인터페이스의 의존할 것을 강조
     * 예시: 스프링에서는 DIP를 지키기 위해 객체를 생성하고 연관관계를 맺어주는 별도의 조립, 설정자(DI, loc 컨테이너)를 제공


### MVC 패턴
 #
 <br>
![ModelViewControllerDiagram](https://github.com/Gabozago-Study/CS-Gabozago/assets/100250055/652ddb16-c1b4-4e59-8e62-c7053a41ad74)

 <br>

 * 웹 개발에서는 MVC 패턴을 사용하여 데이터베이스에 접근하는 모델, 웹 페이지를 표시하는 뷰, 사용자의 입력을 처리하는 컨트롤러로 애플리케이션을 구성
  
 * 애플리케이션의 구성 요소를 세 가지 역할로 나누어 설계하는 방법으로 모델(Model), 뷰(View), 컨트롤러(Controller)로 구성되며 각 역할은 명확하게 역할과 책임을 갖고, 서로 독립적으로 동작
   * 모델(Model): 애플리케이션의 데이터와 비즈니스 로직을 담당 (DAO, DTO, Service 등)
   * 뷰(View): 사용자 인터페이스를 표시하고 사용자 입력을 담당 (html, jsp, thymeleaf 등의 화면 구성)
   * 컨트롤러(Controller): 사용자 입력을 처리하고 모델과 뷰를 연결하여 데이터의 흐름을 제어
 * 장점
   * 유연성: 각 역할이 분리되어 있으므로, 변경이 발생해도 다른 역할에 영향을 미치지 않고 수정이 가능
   * 유지보수성: 코드의 가독성과 유지보수성이 향상
   * 재사용성: 모델과 뷰, 컨트롤러의 분리로 인해 재사용이 용이
 * 단점
   * 대규모 애플리케이션에서는 관리해야 할 코드가 늘어나 복잡해질 수 있음
 * 종류
  
 <img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fw08Lw%2FbtrlbKqhWKO%2FqUYnM7xziHIQUE28L6WBZ1%2Fimg.png" alt="model1">
 
 > Model1: Controller 영역에 View 영역을 같이 구현하는 방식이며, 사용자의 요청을 JSP가 전부 처리

 <img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbGZKd4%2FbtrleqFoykC%2FkXkFFucLJdHJ4hNvfcmav0%2Fimg.png" alt="model2">

> Model2: 웹브라우저 사용자의 요청을 서블릿이 받고 서블릿은 해당 요청으로 View로 보여줄 것인지 Model로 보낼 것인지를 판단하여 전송



 ### MVP 패턴
 #
 * MVC 패턴의 발전된 형태로, 애플리케이션의 구성 요소를 세 가지 역할로 나누어 설계하며 모델(Model), 뷰(View), 프리젠터(Presenter)로 구성
   * 뷰(View): 사용자 인터페이스를 표시하고, 프리젠터를 통해 사용자의 입력을 전달
   * 프리젠터(Presenter): 사용자 입력을 처리하고 모델과 뷰를 연결하여 데이터의 흐름을 제어
 * 장점
   * 유연성: 각 역할이 분리되어 있어 변경이 발생해도 다른 역할에 영향을 미치지 않고 수정이 가능
   * 테스트 용이성: 프리젠터는 인터페이스를 통해 뷰와 모델과 분리되어 있어 단위 테스트가 용이
 * 단점
   * 대규모 애플리케이션에서는 관리해야 할 코드가 늘어나 복잡해질 수 있음
 * 예시
   * 안드로이드 앱 개발에서는 MVP 패턴을 사용하여 뷰(액티비티)와 프리젠터(프레젠터 클래스)를 분리하여 개발

 ### MVVM 패턴
 #
 * 애플리케이션의 구성 요소를 세 가지 역할로 나누어 설계하는 방법으로 모델(Model), 뷰(View), 뷰모델(ViewModel)로 구성
   * 뷰(View): 사용자 인터페이스를 표시하며, 뷰모델과 바인딩하여 데이터를 표시
   * 뷰모델(ViewModel): 뷰와 모델 사이의 매개체 역할을 하며, 뷰의 상태와 모델의 데이터를 뷰에 반영하고, 뷰에서 발생하는 이벤트를 처리
 * 장점
   * 데이터 바인딩: 뷰와 뷰모델의 데이터 바인딩을 통해 UI 업데이트를 간단하게 처리
   * 테스트 용이성: 뷰와 모델의 분리로 인해 단위 테스트가 용이
 * 단점
   * MVVM 패턴은 처음에는 학습이 필요하며, 복잡한 애플리케이션에서 구현하기 어려울 수 있음
 * 예시
   * 개발에서는 MVVM 패턴을 사용하여 Angular 프레임워크에서 컴포넌트와 뷰모델을 분리하여 개발

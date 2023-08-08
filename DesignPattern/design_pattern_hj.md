# Design Pattern

### 개념
#
* 특정 상황에서 공통적으로 발생하는 문제에 쓰이는 재사용 가능한 해결책
* 장점
    * 소프트웨어의 구조를 파악하기 용이
    * 재사용을 통한 개발 시간 단축
    * 설계 변경 시, 비교적 원활한 조치 가능
* 단점
    * 객체 지향 언어에서 사용할 경우, 객체 지향적 설계를 추가로 고려해야 함
    * 초기 투자 비용이 큼

<br/>

### 종류
#
* 생성 패턴
    * 객체 생성과 관련된 패턴
    * 객체의 생성과 조합을 캡슐화해 특정 객체가 생성되거나 변경되어도 프로그램 구조에 영향을 크게 받지 않도록 유연성을 제공
* 구조 패턴
    * 프로그램 구조를 설계하는데 사용되는 패턴
    * 클래스나 객체를 조합해 더 큰 구조를 만드는 패턴
* 행위 패턴
    * 객체나 클래스 사이의 알고리즘 또는 책임 분배에 관련된 패턴
    * 결합도를 최소화하는 것이 주 목적

<br/>

### 대표적인 생성 패턴
#
* Singleton Pattern
    * 단 하나의 객체를 생성하고 생성된 객체를 어디서든 참조할 수 있도록 하는 패턴
    * 클래스를 static으로 선언하는 것이 아닌, 동적으로 생성하고 heap 영역에서 GC로 관리되도록 하되, 단 하나의 객체를 생성
    * 예시
        ```Java
        public class Singleton {
            private static Singleton instance;
            private Singleton() {}
            public static Singleton getInstance()
                if(instance == null) {
                    instance = new Singleton();
                }
                return instance;
        }

        public class AnotherClass {
            void usingSingleton() {
                Singleton inst = Singleton.getInstance();
            }
        }
        ```
    * 사용 예시: DB Connection, Thread Pool

* Builder Pattern
    * 인스턴스를 생성자를 통해 직접 생성하지 않고, 빌더라는 내부 클래스를 통해 간접적으로 생성하게 하는 패턴
    * 예시
        ```Java
        class StudentBuilder {
            private int id;
            private String name;
            private String grade;
            private String phoneNumber;

            public StudentBuilder id(int id) {
                this.id = id;
                return this;
            }

            public StudentBuilder name(String name) {
                this.name = name;
                return this;
            }

            public StudentBuilder grade(String grade) {
                this.grade = grade;
                return this;
            }

            public StudentBuilder phoneNumber(String phoneNumber) {
                this.phoneNumber = phoneNumber;
                return this;
            }

            public Student build() {
                // Student 생성자 호출
                return new Student(id, name, grade, phoneNumber);
            }
        }

        public static void main(String[] args) {

            Student student = new StudentBuilder()
                        .id(2016120091)
                        .name("임꺽정")
                        .grade("Senior")
                        .phoneNumber("010-5555-5555")
                        .build();

            System.out.println(student);
        }
        ```

* Factory Method
    * 추상 클래스에는 객체를 생성하는 추상 메서드를 정의하고, 이를 하위 클래스에서 구현하여 원하는 타입의 객체를 생성
    * 의존성과 결합도를 낮출 수 있음
    * 예시
        * 슈퍼 클래스, AnimalFactory - 추상 메서드 createAnimal() 보유
        * 하위 클래스, (DogFactory, CatFactory) - createAnimal()을 오버라이드 ▶ Dog와 Cat 인스턴스 생성

* Abstract Factory Method
    * 슈퍼 클래스에서 기본적인 알고리즘의 흐름을 정의하고, 하위 클래스에서 특정 단계를 구현하는 방법
    * 예시
        * 슈퍼 클래스, Algorithm
            - 추상 메서드 step1(), step2(), step3() ...
            - algorithm(): 추상 메서드 step1(), step2(), step3()로 구성된 메서드
        * 하위 클래스, (AlgorithmA, AlgorithmB)
            - step1(), step2(), step3()을 구현하여 algorithm()을 사용

<br/>

### 대표적인 구조 패턴
#
* Adapter Pattern
    * 호환성이 없는 인터페이스 때문에 함께 동작할 수 없는 클래스들을 함께 작동해주도록 변환 역할을 해주는 행동 패턴
    ```Java
    class Adapter implements Target {
        // 호환성이 없어 직접 사용 불가능한 클래스
        Service adaptee;

        Adapter(Service adaptee) {
            this.adaptee = adaptee;
        }

        //Adapter method 호출 시, 기존 서비스인 adaptee medthod로 사용 가능
        public void method(int data) {
            adaptee.specificMethod(data);
        }
    }
    ```

<br/>

### 대표적인 행위 패턴
#
* Observer Pattern
    * 일대다 의존성을 가지며, 분산 이벤트 핸들링 시스템에 주로 사용
    * 한 객체의 상태가 변경되었을 때, 그 객체에 의존하는 다른 객체들에게 자동으로 알림을 보내고 갱신을 요청

* Template Method Pattern
    * 여러 클래스에서 공통으로 사용하는 메서드를 템플릿화 하여 상위 클래스에서 정의하고, 하위 클래스마다 세부 동작 사항을 다르게 구현하는 패턴
    * 사용 예시: Abstract Map

* Strategy Pattern
    * 비슷한 동작을 하지만 다르게 구현되어 있는 행위(전략)들을 공통의 인터페이스를 구현하는 각각의 클래스로 구현하고, 동적으로 바꿀 수 있도록 하는 패턴
    * 코드의 결합도를 낮춰 유지 보수성을 높일 수 있음
    * 예시
        ```Java
        // 전략 인터페이스 (Strategy Interface)
        interface Strategy {
            int execute(int a, int b);
        }

        // 전략 구현 클래스 (Concrete Strategies)
        class AddOperation implements Strategy {
            public int execute(int a, int b) {
                return a + b;
            }
        }

        // 컨텍스트 클래스 (Context)
        class Context {
            private Strategy strategy;

            // 전략 교체 메소드
            public Context(Strategy strategy) {
                this.strategy = strategy;
            }

            // 전략 실행 메소드
            public int executeStrategy(int a, int b) {
                return strategy.execute(a, b);
            }
        }

        // 사용 예시
        public class Main {
            public static void main(String[] args) {
                int a = 10, b = 5;

                // 전략 설정
                Strategy addStrategy = new AddOperation();
                Context context = new Context(addStrategy);

                // 전략 실행
                int result = context.executeStrategy(a, b);
            }
        }
        ```

* Iterator Pattern
    * 일련의 데이터 집합에 대하여 순차적인 접근(순회)을 지원하는 패턴
    * 자바에서 제공하는 Iterator Interface는 ArrayList, TreeSet, HashMap 등 컬렉션 클래스의 요소들을 순회하는 데 사용

<br/>

### MVC Pattern
#
* Model-View-Controller의 약자로 애플리케이션을 세 가지 역할로 구분한 개발 방법론
    * Model
        * 데이터 관리 및 비즈니스 로직을 처리하는 부분
        * DAO, DTO, Service 등
    * View
        * 비즈니스 로직의 처리 결과를 통해 유저 인터페이스가 표현되는 구간
        * html, jsp, thymeleaf 등의 화면 구성
    * Controller
        * 사용자의 요청을 처리하고 Model과 View를 중개하는 역할 
* 종류
<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fw08Lw%2FbtrlbKqhWKO%2FqUYnM7xziHIQUE28L6WBZ1%2Fimg.png" alt="model1">
    * Model1: Controller 영역에 View 영역을 같이 구현하는 방식이며, 사용자의 요청을 JSP가 전부 처리
<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbGZKd4%2FbtrleqFoykC%2FkXkFFucLJdHJ4hNvfcmav0%2Fimg.png" alt="model2">
    * Model2: 웹브라우저 사용자의 요청을 서블릿이 받고 서블릿은 해당 요청으로 View로 보여줄 것인지 Model로 보낼 것인지를 판단하여 전송

<br/>

### 객체 지향 설계 원칙: SOLID
#
* SRP (Single Responsibility Principle) 단일 책임 원칙
    * 하나의 클래스는 하나의 책임만 가져야한다는 원칙
    * SRP를 잘 따르면 응집도(cohesion)는 높이고 결합도(coupling)은 낮출 수 있음
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

<br/>



### 📚 참고 자료
#
https://gmlwjd9405.github.io/2018/07/06/design-pattern.htm <br/>
https://velog.io/@sunhwa508/GOF-%EB%8C%80%ED%91%9C%EC%A0%81%EC%9D%B8-10-%EA%B0%80%EC%A7%80-Design-patterns <br/>
https://github.com/GimunLee/tech-refrigerator/tree/master/Design%20Pattern <br/>
https://inpa.tistory.com/category/%EB%94%94%EC%9E%90%EC%9D%B8%20%ED%8C%A8%ED%84%B4/GOF?page=2 <br/>
https://cocoon1787.tistory.com/733 <br/>
https://flower0.tistory.com/416 <br/>
https://velog.io/@falling_star3/Java-%EA%B0%9D%EC%B2%B4-%EC%A7%80%ED%96%A5-%EC%84%A4%EA%B3%84%EC%9D%98-5%EA%B0%80%EC%A7%80-%EC%9B%90%EC%B9%99-SOLID <br/>
https://dev-coco.tistory.com/163

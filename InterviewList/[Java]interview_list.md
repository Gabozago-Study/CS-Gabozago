# [Java] Interview List

### [Q] OOP란?
#
애플리케이션을 구성하는 요소들을 객체로 바라보고, 객체들을 유기적으로 연결하여 프로그래밍 하는 것을 의미합니다. <br/>
캡슐화, 상속, 다형성, 추상화의 특징을 갖습니다.

### [Q] 캡슐화 방법
#
클래스 내부의 필드는 private로 선언하고 해당 필드에 대해 getter/setter를 public으로 선언하여 외부 접근을 선택적으로 제어하는 방법이 있습니다.

### [Q] 추상클래스와 인터페이스 차이?
#
인터페이스는 2개 이상 구현할 수 있으며, 서로 관련이 없는 클래스에서 공통적으로 사용하는 방식이 필요하지만 기능을 각각 구현할 필요가 있는 경우에 사용합니다. <br/>
추상 클래스는 1개만 상속받을 수 있으며, 오버라이딩을 통한 기능의 구현과 확장을 위해 사용합니다.

### [Q] final이 붙은 클래스와 메서드의 특징
#
final 클래스는 상속할 수 없으며, final 메소드는 재정의할 수 없습니다. <br/>
final 필드는 초기값 설정 후, 프로그램 종료 전까지 수정할 수 없습니다.

### final 필드와 상수 차이
#
final 필드는 객체마다 저장되고, 생성자의 매개값을 통해서 여러가지 값을 가질 수 있지만, 상수는 객체마다 저장할 필요가 없는 공용성을 띠고 있으며, 여러가지 값으로 초기화 될 수 없습니다. <br/>
이러한 상수는 static final로 선언합니다.

### [Q] final, finally과 finalize에 대한 설명
#
final은 변수나 메서드 또는 클래스가 '변경 불가능'하도록 만듭니다. <br/>
finally는 try-catch 블럭에서 선택적으로 사용되며, 반드시 실행되어야 할 구문을 선언하기 위해 사용합니다. <br/>
finalize()는 Garbage Collector가 더 이상의 참조되지 않는 객체를 메모리에서 삭제할 때 호출됩니다.

### [Q] static과 instance 차이
#
instance 멤버는 객체를 생성한 후 사용할 수 있는 필드와 메서드를 말하며, 객체 생성없이 사용할 수 있는 필드와 메서드를 static 멤버라고 합니다. <br/>
객체가 사라지면 멤버도 사라지는 인스턴스 멤버와 달리 클래스 멤버는 프로그램이 종료될 때까지 존재합니다.

### [Q] java의 main 메서드가 static인 이유
#
인스턴스가 없는 클래스의 main()을 호출해야하기 때문에 static으로 선언해야 합니다.

### [Q] Overriding과 Overloading 차이
#
Overriding은 상속 관계에서 부모 클래스의 메서드를 자식 클래스에서 재정의하는 것입니다. <br/>
반면, Overloading은 같은 클래스 내에서 메서드 이름은 동일하지만 매개변수 목록이 다른 여러 개의 메서드를 정의하는 것입니다.

### [Q] Java 프로그램 실행 과정
#
JVM은 OS로부터 메모리(Runtime Data Area)를 할당받습니다. <br/>
이후, 컴파일러(javac)는 소스코드(.java)를 바이트 코드(.class)로 변환합니다. <br/>
이 파일은 JVM의 Class Loader를 통해 Runtime Data Area에 로딩 후, Execution Engine에 의해 해석되어 실행됩니다.

### [Q] Garbage Collection 설명
#
Java 프로세스에서 더 이상 사용하지 않는 동적 할당된 메모리를 자동으로 해제해주는 JVM의 작업입니다.

### [Q] Exception의 분류와 최근에 경험한 Exception과 해결 방안
#
Exception은 크게 CheckedException, UncheckedException으로 구분할 수 있습니다. <br/>
UncheckedException는 RuntimeException 등이 있으며 실행하기 전에 예측할 수 없는 예외로 따로 처리를 하지 않습니다. <br/>
CheckedException은 RuntimeException 이외의 예외로 실행 전 예측 가능한 예외로, 반드시 예외 처리를 해줘야합니다. <br/>
Error는 시스템에 비정상적인 상황에 발생하며 처리할 방법이 없는 것이 특징입니다. <br/>

NullPointException: 객체가 없는 상태에서 객체를 사용할 경우 발생 <br/>
ArrayIndexOutOfBoundsException: 배열에서 인덱스 범위를 초과할 경우 발생 <br/>
NumberFormatException: 숫자로 변환 시, 변환될 수 없는 문자가 포함되어 있을 경우 발생

### [Q] Exception 처리 방법
#
예외처리 구문인 try-catch-finally 블럭을 사용하거나 메소드 선언부 끝에 throws를 선언하여 예외에 대한 처리를 메서드 호출부로 위임할 수 있습니다.

### [Q] 자바에서 제공하는 컬렉션 프레임워크의 주요 인터페이스와 각 특징에 대한 설명
#
List는 순서가 있고, 중복이 허용됩니다. <br/>
Set은 순서가 없고, 중복이 허용되지 않습니다. <br/>
Map은 순서가 없고, Key값에 대한 중복이 허용되지 않습니다.

### [Q] Thread에 대한 설명
#
Thread는 프로세스 내에서 실행되는 흐름의 단위로, 하나의 프로세스는 하나 이상의 스레드를 가지고 스레드를 동시에 실행할 수 있습니다. 이러한 실행방식을 멀티 스레드라고 하며, 자바에서도 이러한 멀티 스레드 방식을 지원하고 있습니다.

### [Q] 동기화와 비동기화에 대한 설명
#
동기화란 하나의 thread가 작업이 끝나기 전에 다른 thread의 접근을 막는 것으로 Thread간 데이터의 간섭,오염을 막을 때 사용합니다. <br/>
비동기화는 현재 실행 중인 명령이 종료되지 않아도 다음 명령 실행 가능한 경우를 말합니다.

### [Q] String, StringBuffer, StringBuilder 차이
#
String은 수정이 불가하므로 수정이 필요할 경우, StringBuffer 또는 StringBuilder를 사용하는 것이 좋습니다.
비동기 처리방식은 StringBuilder와 달리 StringBuffer는 동기 처리 방식을 사용하므로 multiple thread 환경에서 안전합니다.

### [Q] '=='와 'equals()'의 차이
`==`는 참조 비교 방식으로 같은 주소를 가르키고 있는지 확인합니다. 모든 기본 유형(Primitive Types)에 대해 적용할 수 있습니다.
`equals()`는 내용 비교 방식으로 두 객체의 값이 같은지 확인합니다. 이는 기본 유형(Primitive Types)에 대해서는 적용할 수 없습니다.
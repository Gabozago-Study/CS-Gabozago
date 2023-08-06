# Design Pattern
### 디자인 패턴
소프트웨어 코드 작성 시에 생기는 공통적인 문제를 해결하는데 도움이 되는 코드 패턴으로 SW 재사용성, 호환성, 유지 보수성을 보장한다.

### 객체지향 설계 원칙(SOLID)

* Single Responsibility Principle(단일 책임 원칙):
하나의 클래스는 하나의 역할만 해야 함
* Open - Close Principle(개방-폐쇄 원칙):
확장(상속)에는 열려있고, 수정에는 닫혀있어야 함
* Liskov Substitution Principle(리스코프 치환 원칙):
자식이 부모의 자리에 항상 교체될 수 있어야 함
* Interface Segregation Principle(인터페이스 분리 원칙):
인터페이스가 잘 분리되어서 클래스가 필요한 인터페이스만 구현하도록 해야 함
* Dependency Inversion Property(의존관계 역전 원칙):
의존 관계를 만들 때, 구체적인 구현이 아닌 추상화된 인터페이스에 의존해야 함

### 디자인 패턴 종류

생성 패턴: 객체 생성에 관련된 패턴
* 팩토리 메서드 패턴(Factory Method Pattern): 어떤 클래스의 인스턴스를 만들지는 서브 클래스에서 결정하는 패턴
* 싱글턴 패턴(Singleton Pattern): 오직 인스턴스를 하나만 만들어서 재사용하는 패턴
* 빌더 패턴(Builder Pattern): 생성(construction)과 표기(representation)를 분리해 복잡한 객체를 생성하는 패턴
  
구조 패턴: 클래스나 객체를 조합해 더 큰 구조를 만드는 패턴
* 데코레이터 패턴(Decorator Pattern): 원본에 장식을 더하는 데코레이터를 통해서 객체의 결합을 통해 반환 값에 장식을 덧붙이는 패턴
* 프록시 패턴(Proxy Pattern): 대신해서 그 역할 수행하는 프록시를 통해서 메서드의 반환 값을 수정하는 게 아니라 별도 로직을 수행하는 패턴
* 어댑터 패턴(Adapter Pattern): 객체를 속성으로 참조해서 만드는 패턴으로 호출 당하는 쪽의 메서드를 호출하는 쪽의 코드에 대응하도록 변환기를 통해 호출하는 패턴
  
행위 패턴: 클래스나 객체들이 서로 상호 작용하는 방법이나 책임 분배 방법을 정의하는 패턴
* 옵저버 패턴(Observer Pattern): 한 객체의 상태 변화를 관찰하다가 변화가 있을 때마다 옵저버 목록에 있는 옵저버들에게 변화를 알려주는 패턴으로 일대다 객체 의존 관계를 구성하는 패턴
* 템플릿 메서드 패턴(Template Method Pattern): 상위 클래스의 템플릿 메서드에서 하위 클래스가 오버라이딩한 메서드를 호출하는 패턴
* 전략 패턴(Strategy Pattern): 클라이언트가 전략을 생성해 전략을 실행한 컨텍스트에 주입하는 패턴


#
## 대표적인 생성 패턴
### 빌더 패턴
생성(construction)과 표기(representation)를 분리해 복잡한 객체를 생성하는 패턴(생성 패턴). 

필요한 데이터만 설정할 수 있고, 유연성을 확보,
가독성을 높일 수 있고, 변경 가능성을 최소화할 수 있다.


```java 
public class PizzaBuilder {
 
    private final String name;
    private final String dough;
    private final String sauce;
    private final String topping;
    private final int price;
 
 
    // 객체 생성 전, 값을 세팅해줄 Builder 내부 클래스
    public static class Builder {
        private String name;
        private String dough;
        private String sauce;
        private String topping;
        private int price;
 
        public Builder name(String name) {
            this.name = name;
            return this;
        }
 
        public Builder dough(String dough) {
            this.dough = dough;
            return this;
        }
 
        public Builder sauce(String sauce) {
            this.sauce = sauce;
            return this;
        }
 
        public Builder topping(String topping) {
            this.topping = topping;
            return this;
        }
 
        public Builder price(int price) {
            this.price = price;
            return this;
        }
 
         public PizzaBuilder build() {
            return new PizzaBuilder(this);
         }
    }
 
    public PizzaBuilder(Builder builder) {
        this.name = builder.name;
        this.dough = builder.dough;
        this.sauce = builder.sauce;
        this.topping = builder.topping;
        this.price = builder.price;
    }
 
    @Override
    public String toString() {
        return "name: " + name + ", " + "dough: " + dough + ", " + "sauce: " + sauce + ", " + "topping: " + topping + "price: " + price;
    }  
}

public class Main {
 
    // 빌더 패턴 사용
    PizzaBuilder pizzaBuilder = new PizzaBuilder.Builder()
            .name("하와이언피자")
            .dough("thin")
            .sauce("핫소스")
            .topping("페퍼로니")
            .price(20000)
            .build();
}

```
> **클래스 또는 생성자에 @Builder 애노테이션을 붙여주면 빌더 패턴 코드가 빌드된다.**
>```java 
>@Builder
>public class Bag {
>	private String name;
>        private int money;
>        private STring memo;
>} 
>Bag bag = Bag.builder()
>		.name("name")
>        	.money(1000)
>        	.memo("memo")
>        	.build();
>```
>   
>

### 싱글톤 패턴
한번의 객체 생성으로 재사용이 가능하기 때문에 메모리 낭비를 방지하고 객체가 전역성을 띄기 때문에 공유가 용이함
```java 
public class Singleton {

    static Singleton singletonObject;

    private Singleton() {};

    public static Singleton getInstance() {
        if (singleObject == null) {
            singletonObject = new Singleton();
        }
        return singletonObject;
    }
}
```

### 팩토리 메서드 패턴
클래스의 인스턴스를 만드는 것을 서브 클래스에서 결정하는 패턴으로 팩토리 메서드 패턴과 추상 팩토리 패턴으로 구체화되나 주로 팩토리 메서드 패턴를 사용. 
> 차이점은 팩토리 메서드 패턴은 구체적인 객체 생성 과정을 하위 또는 구체적인 클래스로 옮기는 것이 목적이고,
추상 팩토리 패턴은 관련있는 여러 객체를 구체적인 클래스에 의존하지 않고 만들 수 있게 해주는것이 목적
```java 
abstract class Coffee {

    // 팩터리 메서드
	public abstract int getPrice();

	@Override
	public String toString() {
		return "Hi this coffee is " + this.getPrice();
	}
}

class CoffeeFactory {
	public static Coffee getCoffee(String type, int price) {
		if ("Latte".equalsIgnoreCase(type))
			return new Latte(price);
		else if ("Americano".equalsIgnoreCase(type))
			return new Americano(price);
		else {
			return new DefaultCoffee();
		}
	}
}
class Americano extends Coffee {
	private int price;

	public Americano(int price) {
		this.price = price;
	}

	@Override
	public int getPrice() {
		return this.price;
	}
}

class Latte extends Coffee {
	private int price;

	public Latte(int price) {
		this.price = price;
	}

	@Override
	public int getPrice() {
		return this.price;
	}
}

public class TestApplication {
	public static void main(String[] args) {
		Coffee latte = CoffeeFactory.getCoffee("Latte", 4000);
		Coffee americano = CoffeeFactory.getCoffee("Americano", 3000);
		System.out.println("Factory latte ::" + latte);
		System.out.println("Factory americano ::" + americano);
	}
}
```


#
## 대표적인 구조 패턴
### 프록시 패턴
대신해서 그 역할 수행하는 프록시를 통해서 메서드의 반환 값을 수정하는 게 아니라 별도 로직을 수행하는 패턴(구조 패턴)
``` java
public interface IService {
    String runSomething();
}
public class ServiceA implements IService {
    public String runSomething() {
        return "서비스";
    }
}
public class Proxy implements IService {
    IService service;

    public String runSomething() {
        System.out.println("호출에 대한 흐름 제어가 목적, 반환 값은 그대로");
        service = new ServiceA();
        return service.runSomething();
    }
}
public class ClientWithProxy {
    // 프록시를 이용한 호출
    IService proxy = new Proxy();
    System.out.println(proxy.runSomething());
}
```

### 어댑터 패턴
객체를 속성으로 참조해서 만드는 패턴으로 호출 당하는 쪽의 메서드를 호출하는 쪽의 코드에 대응하도록 어댑터 통해 호출하는 패턴(구조 패턴), 어댑터는 서로 다른 두 인터페이스 사이에 통신이 가능하게 하는 것

``` java
// Adaptee : 클라이언트에서 사용하고 싶은 기존의 서비스 (하지만 호환이 안되서 바로 사용 불가능)
class Service {

    void specificMethod(int specialData) {
        System.out.println("기존 서비스 기능 호출 + " + specialData);
    }
}

// Client Interface : 클라이언트가 접근해서 사용할 어댑터 모듈
interface Target {
    void method(int data);
}

// Adapter : Adaptee 서비스를 클라이언트에서 사용하게 할 수 있도록 호환 처리 해주는 어댑터
class Adapter implements Target {
    Service adaptee; // composition으로 Service 객체를 클래스 필드로

    // 어댑터가 인스턴스화되면 호환시킬 기존 서비스를 설정
    Adapter(Service adaptee) {
        this.adaptee = adaptee;
    }

    // 어댑터의 메소드가 호출되면, Adaptee의 메소드를 호출하도록
    public void method(int data) {
        adaptee.specificMethod(data); // 위임
    }
}

class Client {
    public static void main(String[] args) {
        // 1. 어댑터 생성 (기존 서비스를 인자로 받아 호환 작업 처리)
        Target adapter = new Adapter(new Service());

        // 2. Client Interfac의 스펙에 따라 메소드를 실행하면 기존 서비스의 메소드가 실행된다.
        adapter.method(1);
    }
}
```


#
## 대표적인 행위 패턴
### 템플릿 메서드 패턴
상위 클래스의 템플릿 메서드에서 하위 클래스가 오버라이딩한 메서드를 호출하는 패턴(행위 패턴)으로 
상속을 이용해서 동일한 코드를 제외하고 코드를 추가
``` java
abstract class Ramyun {
    public void cook() {
        System.out.println("불을 켠다.");
        System.out.println("냄비에 물을 받고 끓인다.");

        getRamyun();

        System.out.println("스프와 면을 넣는다.");
        System.out.println("알맞게 끓인다.");
    }

    protected abstract void getRamyun();
}
// JinRamyun.java
public class JinRamyun extends Ramyun {
    @Override
    protected void getRamyun() {
        System.out.println("진라면을 준비한다.");
    }
}

// SamyangRamyun.java
public class SamyangRamyun extends Ramyun {
    @Override
    protected void getRamyun() {
        System.out.println("삼양라면을 준비한다.");
    }
}
```



## MVC 패턴
 Model, View, Controller의 약자로, 하나의 애플리케이션, 프로젝트를 구성할 때 그 구성요소를 세가지의 역할로 구분한 패턴
 <br>
![ModelViewControllerDiagram](https://github.com/Gabozago-Study/CS-Gabozago/assets/100250055/377a1dd0-b600-46ef-9aa7-7e0da88d06f4)
 <br>

Model
* 데이터를 가진 객체
* 사용자가 편집하길 원하는 모든 데이터를 가지고 있어야 함
* 뷰나 컨트롤러에 대해서 어떤 정보도 알지 말아야 함
* 재사용가능해야 하며 다른 인터페이스에서도 변하지 않아야 함
* 변경이 일어나면, 변경 통지에 대한 처리방법을 구현해야 함


View
* 사용자가 볼 결과물을 생성하기 위해 모델로부터 정보를 얻어옴
* 모델이 가지고 있는 정보를 따로 저장하지 않음
* 모델이나 컨트롤러와 같이 다른 구성요소들을 몰라야 함
* 재사용가능하게끔 설계를 해야 하며 다른 정보들을 표현할 때 쉽게 설계를 해야 함
* 변경이 일어나면, 변경 통지에 대한 처리방법을 구현해야 함
  
Controller
* 데이터와 사용자인터페이스 요소들을 잇는 다리역할. 즉, 사용자가 접근한 URL에 따라 사용자의 요청사항을 파악한 후에 그 요청에 맞는 데이터를 Model을 의뢰하고, 데이터를 View에 반영해서 사용자에게 알려줌
* 모델이나 뷰에 대해서 알고 있고, 모델이나 뷰의 변경을 모니터링 해야 함
* 애플리케이션의 메인 로직은 컨트롤러가 담당

> ### *왜 MVC 패턴을 사용해야 할까?*
> 
> 사용자가 보는 페이지, 데이터처리, 그리고 이 2가지를 중간에서 제어하는 컨트롤, 이 3가지로 구성되는 하나의 애플리케이션을 만들면 서로 분리되어 각자의 역할에 집중할 수 있다.
>  
> 비즈니스 로직과 UI로직을 분리하여 유지보수를 독립적으로 수행가능하고, Model과 View가 다른 컴포넌트들에 종속되지 않아 애플리케이션의 확장성, 유연성에 유리하며, 중복 코딩의 문제점이 제거된다.
>
> 그러나 Controller에 다수의 Model과 View가 복잡하게 연결되어 있는 상황이 발생할 수 있는 한계가 존재한다. 

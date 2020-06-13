## Introduction

유연하고 재사용 가능한 설계를 하는 것은 매우 어려운 일이다.

1. 문제 속에서 적절한 책임을 가진 객체를 뽑아내고,
2. 이들이 어떤 인터페이스를 가지고 서로 협력하는지를 정의해야 한다.
3. 1과 2가 현재 주어진 비즈니스 요구사항을 해결할 만큼 specific 해야 하며, 동시에 이후에 발생할 요구사항의 변경에도 기민하게 대응할 수 있을 만큼 general 해야 한다.

이런 설계를 잘 해내는 노련한 객체지향 설계자들은 매 문제마다 새로운 솔루션을 만들기 보다는 기존에 잘 동작했던 솔루션을 재활용한다.

→ 디자인 패턴이란 이렇게 반복적으로 나타나는 패턴을 정리하고 기록하고 명명한 것이다.

디자인 패턴은 옳은 설계에 더 빠르게 도달하는 데에 도움을 준다.

- 새로운 시스템을 설계할 때 재사용성이 좋은 설계를 하도록 도와준다.
- 기존 시스템에 대해서는 클래스와 클래스간의 상호작용에 대한 명세, 그리고 이들에 담긴 의도를 더 명확하게 표현함으로써 다큐멘테이션과 유지보수를 도와준다.
- 디자인 패턴을 적용하면 많은 design decision이 자연스럽게 내려진다. (이 선택이 맞는지 틀린지 고민할 필요 없이 확신을 가지게 해준다)


## What is a Design Pattern?

> Each pattern describes a problem which occurs over and over again in our environment, and then describes the core of the solution to that problem, in such a way that you can use this solution a million times over, without ever doing it the same way twice.
>
> \- Christopher Alexander

디자인 패턴은 네 가지 요소로 구성되어 있다.

- Pattern name - 패턴의 이름. 패턴의 이름이 중요한 이유는 더 높은 단계의 추상화 계층에서 소프트웨어를 설계할 수 있도록 해주기 때문이다.  이는 커뮤니케이션(동료와의 논의, 다큐멘테이션)의 효율성을 높여준다.
- Problem - 패턴을 언제 적용해야 하는지. 문제 상황과 컨텍스트를 설명한다.
- Solution - 설계를 구성하는 요소, 각 요소들 사이의 관계, 책임, 그리고 상호작용. 패턴은 여러 상황에 적용할 수 있는 템플릿과 같아야 하기 때문에 구체적인 설계나 구현 방식을 제시하지는 않는다. 대신, 패턴은 문제에 대한 추상적인 분석과, 각 요소들의 책임이 이 문제를 어떻게 해결해주는지를 설명해준다.
- Consequence - 패턴을 적용했을 때의 결과와 장단점. 이는 내가 처한 상황에 대해 패턴을 적용하는 것이 얼마나 좋은지 평가할 수 있게 해준다. Consequences는 주로 다음과 같은 요소를 고려한다:
    - 시간/공간적 트레이드 오프
    - 실제로 구현이 얼마나 어려운가
    - 시스템의 유연성, 확장성, 이식 가능성

**The design patterns in this book are descriptions of communicating objects and classes that are customized to solve a general design problem in a particular context.**

이 책에서 디자인 패턴에 대한 예제를 작성할 때 사용하는 언어는 C++과 SmallTalk이다. 언어 선택이 중요한 이유는 같은 패턴이라도 언어에서 제공하는 기능에 따라 구현이 어려운 정도가 다르기 때문이다. 만약 절차 지향적인 언어를 골랐으면 encapsulation, polymorphism과 같은 단어 자체가  하나의 패턴이 됐을 수도 있다.


## Organizing the Catalogs
이 책에서는 디자인 패턴을 두 축으로 구분한다.

- purpose - 패턴이 어떤 일을 하는지.
    - creational - 객체 생성과 관련된 패턴.
    - structural - 객체를 조합하는 방법과 관련된 패턴.
    - behavioral - 객체의 책임과 객체 사이의 상호작용을 정의하는 패턴.
- scope - class에 적용되는지, object에 적용되는지.
    - class pattern - 부모와 자식 클래스 사이의 관계에 대한 패턴. compile time에 static하게 결정된다.
    - object pattern - 객체 사이의 관계에 대한 패턴. run-time에 dynamic 하게 변경될 수 있다.

→ 총 6개의 카테고리가 생성된다.

> Creational class patterns defer some part of object creation to subclasses, while Creational object patterns defer it to another object. The Structural class patterns use inheritance to compose classes, while the Structural object patterns describe ways to assemble objects. The Behavioral class patterns use inheritance to describe algorithms and flow of control, whereas the Behavioral object patterns describe how a group of objects cooperate to perform a task that no single object can carry out alone.

## How Design Patterns Solve Design Problems
### Finding Appropriate Objects

* 객체: 데이터 + 메소드
* 메소드: 객체가 가지고 있는 데이터를 다루는 절차
* 클라이언트: 이 객체를 사용하는 다른 객체
* 메세지: 클라이언트가 다른 객체에게 메소드를 특정 인자와 함께 실행시켜 달라고 하는 요청

객체지향 설계에서 어려운 점은 시스템을 어떤 객체들로 나눌지를 결정하는 일이다. 이 선택에는 encapsulation, granularity, dependency, flexibility, performance, evolution, reusability 등의 수많은 기준이 관여하는데, 각각의 기준이 종종 상충하기 때문이다.

보통 현실 세계를 그대로 반영하는 방식으로 객체를 설계하는데, **이러한 방식은 오늘의 현실에는 잘 들어 맞지만 내일의 현실에 대해서는 그렇지 않을 가능성이 높다.** 그래서 많은 객체지향 설계는 종종 현실에는 존재하지 않는 객체를 포함하게 된다. 이런 추상이 설계를 유연하게 만드는 핵심이다.

> Strict modeling of the real world leads to a system that reflects today's realities but not necessarily tomorrow's.

디자인 패턴은 바로 이런 덜 자명하고 덜 명확한 객체와 추상을 드러나게 도와준다.

### Determining Object Granularity

> Objects can vary tremendously in size and number. They can represent everything down to the hardware or all the way up to entire applications. How do we decide what should be an object?

객체는 하드웨어 수준에서부터 하나의 어플리케이션까지 엄청나게 넓은 범위의 것들을 표현할 수 있기 때문에, 객체의 크기를 결정하는 것은 어려운 일이다. 디자인 패턴은 각 상황에서 객체를 어떤 크기와 갯수로 만들어야 하는지를 결정하는 데에 도움을 준다.

### Specifying Object Interfaces

* 메소드의 signiture - 메소드 이름 + 파라미터, + 리턴 값
* 인터페이스 - 메소드의 집합
* 타입 - 특정 인터페이스를 부르는 이름
* 서브타입 - 특정 타입의 메소드를 모두 포함하는 타입

인터페이스는 객체지향 시스템의 뼈대다. 객체는 오로지 인터페이스를 통해서만 외부 세계와 소통한다. 객체는 인터페이스의 메소드를 자유롭게 구현할 수 있다. 따라서 같은 인터페이스를 가진 두 객체는 완전히 다른 행동을 할 수 있다. 이렇게 요청을 처리할 객체를 런타임에 결정하는 것을 동적 바인딩이라 한다.

다형성이란 같은 인터페이스를 가진 객체들끼리 서로 대체할 수 있는 성질이다. 다형성은 클라이언트가 객체의 구현이 아닌 인터페이스에만 의존하기 때문에, 클라이언트가 특정 구현에 종속되지 않게 도와주며 객체들의 결합도를 낮춘다.

디자인 패턴은 객체의 인터페이스를 정의하는 데에 도움을 준다.

- 인터페이스가 가져야 하는 핵심 operation 과 해당 operation 에서 주고받을 데이터를 찾아내는 데에 도움을 준다.
- 인터페이스에 어떤 것을 포함하면 안 되는지를 명시하는 경우도 있다. 
- 인터페이스와 인터페이스의 관계를 명시하기도 한다.

### Specifying Object Implementations

클래스 상속은 부모 클래스의 데이터와 메소드를 모두 포함하는 새로운 클래스를 정의하는 것이며, 상속받은 클래스는 부모 클래스의 메소드를 오버라이딩할 수 있다.

추상 클래스란 서브 클래스들의 공통 인터페이스이다. 추상 클래스는 일부 메소드의 구현을 서브 클래스에게 맡기며, 해당 메소드의 구현이 되어있지 않기 때문에 인스턴스화 할 수 없다.

믹스인 클래스는 다중 상속을 통해 다른 클래스들이 기능을 확장할 수 있게 해준다.

### Class versus Interface Inheritance

클래스는 객체의 내부 상태와 메소드의 구현을 정의하지만, 타입은 객체의 구현과 관계없이 인터페이스에 의해 정의된다. 즉 한 객체는 다양한 타입을 가질 수 있고, 서로 다른 클래스의 객체는 같은 타입을 가질 수 있다.

클래스 상속과 인터페이스 상속의 차이

* 클래스 상속: 이미 정의된 객체의 구현을 재활용하는 것
* 인터페이스 상속 (서브타이핑):  상속된 인터페이스의 구현체는 부모 인터페이스 구현체로도 사용할 수 있는 것

이 두 가지 컨셉을 헷갈리기 쉬운데, 많은 언어가 두 가지를 구분하지 않고 있기 때문이다. 예를 들어, C++ 의 상속은 클래스 상속과 인터페이스의 상속이 동시에 일어난다. 그러나 많은 디자인 패턴은 이 둘을 명확히 구분한다.

### Programming to an Interface, not an Implementation

클래스 상속은 기존 클래스를 기반으로 새로운 클래스를 만드는 기법으로, 기존의 구현을 쉽게 재사용할 수 있다. 또한 같은 인터페이스를 가진 여러 객체군을 정의할 수 있게 해주는데, 이는 다형성의 기반이 된다.

모든 클래스는 추상 클래스만 상속해야 하는데, 그래야 부모 클래스의 구현을 가리지 않기 때문이다. 모든 서브클래스들은 추상 클래스의 인터페이스의 요청에 응답할 수 있고, 그렇기에 추상 클래스의 서브타입이 된다.

추상 클래스에 정의된 인터페이스만으로 객체와 상호작용하면 2가지 장점이 존재한다.

1. 클라이언트는 객체가 인터페이스 서브타입이기만 하면 상호작용할 수 있다.
2. 클라이언트는 객체의 구현과 상관없이 상호작용할 수 있다. 

이는 서브시스템간의 의존성을 크게 낮춰준다. 이는 다음과 같은 재사용 가능한 객체지향 설계의 원칙을 제시한다.

> Program to an interface, not an implementation.
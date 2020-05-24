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

---
title: CSharp 객체지향
created: 2024-02-23 10:06
alias:
tags:
---
C#에서 객체 지향 프로그래밍(OOP)을 구현하는 것은 코드의 재사용성, 확장성, 유지보수성을 향상시키는 데 중요합니다. 여기서는 C#을 사용한 간단한 객체 지향 프로그래밍 예제를 통해 클래스, 상속, 인터페이스, 다형성 등의 기본적인 OOP 개념을 설명하겠습니다.

###### csharp 기본 클래스 정의와 인스턴스 생성
![[csharp 기본 클래스 정의와 인스턴스 생성]]


# csharp 인터페이스와 다형성

다음으로, 인터페이스를 사용한 다형성의 예를 들어보겠습니다. `IWalkable` 인터페이스를 정의하여 걷는 행위를 추상화하고, `Dog` 클래스가 이 인터페이스를 구현하도록 하겠습니다.

```csharp
public interface IWalkable
{
    void Walk();
}

public class Dog : Animal, IWalkable
{
    public Dog(string name) : base(name) { }

    public override void Speak()
    {
        Console.WriteLine($"{Name} says: Woof!");
    }

    public void Walk()
    {
        Console.WriteLine($"{Name} is walking.");
    }
}

class Program
{
    static void Main(string[] args)
    {
        Dog myDog = new Dog("Buddy");
        myDog.Speak();
        myDog.Walk();
    }
}
```

이 예제에서 `Dog` 클래스는 `IWalkable` 인터페이스를 구현하여 `Walk` 메소드를 정의합니다. 
이는 `Dog` 클래스가 `IWalkable` 인터페이스의 계약을 준수하며, 걷는 행위를 구체적으로 정의해야 함을 의미합니다. 

이처럼 C#에서 객체 지향 프로그래밍을 활용하면, 
	코드의 재사용성을 높이고, 
	유지보수를 용이하게 하며, 
	시스템의 다양한 부분들 사이의 결합도를 낮추는 등 여러 이점을 얻을 수 있습니다.


###### csharp property
![[csharp property]]



###### csharp 콜론`` 키워드
![[csharp 상속]]


### C#에서의 상속과 인터페이스 구현

C#:
```csharp
public class Dog : Animal, IWalkable
{
    public Dog(string name) : base(name) { }
    // 클래스 구현
}
```

이 코드에서 `Dog` 클래스는 `Animal` 클래스로부터 상속받고(`: Animal`), `IWalkable` 인터페이스를 구현합니다(`, IWalkable`). 
`: base(name)`는 부모 클래스(`Animal`)의 생성자를 호출하는 부분으로, Java의 `super(name);`에 해당합니다.

### Java에서의 상속과 인터페이스 구현 비교

Java에서는 클래스 상속을 위해 `extends` 키워드를 사용하고, 인터페이스 구현을 위해 `implements` 키워드를 사용합니다. 
클래스가 여러 인터페이스를 구현하는 경우, 인터페이스 이름들을 `implements` 키워드 뒤에 콤마로 구분하여 나열합니다.

C#은 이 두 가지 개념(상속과 인터페이스 구현)을 구분하기 위해 별도의 키워드를 사용하지 않고, 콜론을 통해 통합적으로 표현합니다. 
이는 [[csharp의 문법]]적 특징 중 하나이며, 클래스의 상속과 인터페이스 구현을 동시에 간결하게 나타낼 수 있는 방법입니다.


Java에서는 클래스 간의 다중 상속을 허용하지 않는 것이 맞습니다. 
이는 [[다이아몬드 문제]]를 방지하기 위한 설계 결정입니다. 
Java에서는 클래스가 하나의 클래스만 상속받을 수 있지만, 
인터페이스는 여러 개 구현할 수 있어서, 이를 통해 다형성을 제공합니다.

C#에서는 이와 유사한 원칙을 따릅니다. 
C#도 클래스 간의 다중 상속을 허용하지 않습니다. 즉, 한 클래스가 둘 이상의 기반 클래스로부터 직접 상속받는 것은 불가능합니다. 
그러나 C#은 인터페이스를 통해 다형성과 유연성을 제공하며, 한 클래스가 여러 인터페이스를 구현할 수 있도록 합니다. 이는 다중 상속의 일부 이점을 제공하면서도, 다이아몬드 문제와 같은 복잡성을 피할 수 있는 방법입니다.

### C#의 인터페이스 다중 구현 예시:

```csharp
public interface IWalkable
{
    void Walk();
}

public interface IRunnable
{
    void Run();
}

public class Dog : Animal, IWalkable, IRunnable
{
    public void Walk()
    {
        Console.WriteLine("Dog is walking.");
    }

    public void Run()
    {
        Console.WriteLine("Dog is running.");
    }
}
```

이 예시에서 `Dog` 클래스는 `Animal` 클래스로부터 상속을 받으면서, `IWalkable`과 `IRunnable` 두 인터페이스를 구현합니다. 이로써 `Dog` 클래스는 `Walk`와 `Run` 두 메소드를 갖게 되며, 다형성을 활용할 수 있습니다.

C#과 Java 모두 다중 상속의 문제를 피하기 위해 인터페이스를 활용하는 방법을 채택하고 있으며, 이를 통해 개발자가 다형성을 보다 안전하고 효율적으로 사용할 수 있도록 돕고 있습니다.

###### csharp 인터페이스 명명규칙
![[csharp 인터페이스 명명규칙]]

csharp 명명규칙
java랑 다른 점은 메서드 이름에 파스칼 케이스
근데 다울에선 그냥 카멜케이스 쓰네. 카멜케이스 써도 상관없는듯.

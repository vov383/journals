---
title: csharp 기본 클래스 정의와 인스턴스 생성
created: 2024-02-23 10:19
alias:
tags:
---
먼저, 간단한 `Animal` 클래스를 정의하고, 이를 확장하는 `Dog` 클래스를 만들어 보겠습니다. `Animal` 클래스는 모든 동물이 가지고 있을 법한 기본적인 속성과 메소드를 가지며, `Dog` 클래스는 `Animal` 클래스로부터 상속받아 좀 더 특화된 속성이나 행위를 추가합니다.

```csharp
using System;

// 기본 클래스 정의
public class Animal
{
    public string Name { get; set; }
    
    public Animal(string name)
    {
        Name = name;
    }

    public virtual void Speak()
    {
        Console.WriteLine("An animal makes a sound.");
    }
}

// 상속을 통한 확장
public class Dog : Animal
{
    public Dog(string name) : base(name) { }

    public override void Speak()
    {
        Console.WriteLine($"{Name} says: Woof!");
    }
}

class Program
{
    static void Main(string[] args)
    {
        Animal myAnimal = new Animal("Generic Animal");
        myAnimal.Speak();
        
        Dog myDog = new Dog("Buddy");
        myDog.Speak();
    }
}
```

이 예제에서는 `Animal` 클래스에 `Name` 속성과 `Speak` 메소드를 정의했습니다. `Dog` 클래스는 `Animal` 클래스로부터 상속받아 `Speak` 메소드를 오버라이드(재정의)하여 구체적인 동작을 구현했습니다.


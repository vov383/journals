---
title: 패턴 매칭 in CSharp
created: 2024-05-30 08:36
aliases: [패턴 매칭]
tags: [CSharp]
---
변수의 타입과 값을 검사하여 
특정 조건에 따라 로직을 수행할 수 있게 하는 기능입니다. 
이는 조건문과 스위치 문에서 사용될 수 있으며, 
특히 최신 버전의 C#에서는 다양한 패턴 매칭 기능이 추가되었습니다.

#### 1. 기본 패턴 매칭

##### 타입 패턴
타입 패턴은 변수의 타입을 검사하고, 해당 타입으로 변환합니다.

```csharp
object obj = "Hello, World!";
if (obj is string str)
{
    Console.WriteLine(str); // 출력: Hello, World!
}
```

##### 상수 패턴

상수 패턴은 변수가 특정 값과 일치하는지 검사합니다.

```csharp
int number = 5;
if (number is 5)
{
    Console.WriteLine("Number is 5");
}
```

#### 2. 스위치 표현식

스위치 표현식은 간결하게 여러 조건을 처리할 수 있는 새로운 구문입니다.

```csharp
int number = 3;
string description = number switch
{
    1 => "One",
    2 => "Two",
    3 => "Three",
    _ => "Unknown"
};
Console.WriteLine(description); // 출력: Three
```

#### 3. 조건 패턴 (property pattern)

조건 패턴은 객체의 속성을 검사하여 조건을 만족하는지 확인합니다.

```csharp
public class Person
{
    public string Name { get; set; }
    public int Age { get; set; }
}

Person person = new Person { Name = "John", Age = 30 };

if (person is { Age: >= 18 })
{
    Console.WriteLine($"{person.Name} is an adult."); // 출력: John is an adult.
}
```

#### 4. 튜플 패턴

튜플 패턴은 튜플의 각 요소를 검사하여 조건을 만족하는지 확인합니다.

```csharp
(int x, int y) point = (3, 4);

string quadrant = point switch
{
    ( > 0, > 0) => "Quadrant 1",
    ( < 0, > 0) => "Quadrant 2",
    ( < 0, < 0) => "Quadrant 3",
    ( > 0, < 0) => "Quadrant 4",
    _ => "On an axis"
};

Console.WriteLine(quadrant); // 출력: Quadrant 1
```

#### 5. 패턴 조합

여러 패턴을 조합하여 더 복잡한 조건을 처리할 수 있습니다.

```csharp
public class Shape
{
    public double Radius { get; set; }
    public double Width { get; set; }
    public double Height { get; set; }
}

Shape shape = new Shape { Radius = 5 };

string shapeType = shape switch
{
    { Radius: > 0 } => "Circle",
    { Width: > 0, Height: > 0 } => "Rectangle",
    _ => "Unknown"
};

Console.WriteLine(shapeType); // 출력: Circle
```

### 요약
#### 패턴 매칭의 주요 기능
1. **타입 패턴**: 변수의 타입을 검사하고 변환.
2. **상수 패턴**: 변수의 값이 특정 상수와 일치하는지 검사.
3. **스위치 표현식**: 간결하게 여러 조건을 처리.
4. **조건 패턴**: 객체의 속성을 검사하여 조건을 만족하는지 확인.
5. **튜플 패턴**: 튜플의 각 요소를 검사.
6. **패턴 조합**: 여러 패턴을 조합하여 복잡한 조건을 처리.

Q1:
패턴 매칭을 사용할 때 성능 상의 이점과 주의해야 할 점은 무엇입니까?

Q2:
패턴 매칭을 사용하여 복잡한 객체의 상태를 검사할 때의 실제 사례를 설명해 주세요.
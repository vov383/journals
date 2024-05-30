---
title: when 키워드 in CSharp
created: 2024-05-30 08:39
aliases: [when 키워드]
tags: [CSharp]
---
C#의 [[패턴 매칭 in CSharp|패턴 매칭]]과 결합하여 
조건부 논리를 추가할 수 있게 해주는 기능입니다. 
이는 스위치 문과 스위치 표현식에서 사용되며, 
특정 조건을 만족하는 경우에만 해당 케이스가 실행되도록 합니다.

#### `when` 키워드 사용 예제

##### 스위치 문에서의 `when`

```csharp
int number = 10;

switch (number)
{
    case int n when n > 0:
        Console.WriteLine("Positive number");
        break;
    case int n when n < 0:
        Console.WriteLine("Negative number");
        break;
    default:
        Console.WriteLine("Zero");
        break;
}
```

이 예제에서 `number`가 0보다 크면 "Positive number"를 출력하고, 
0보다 작으면 "Negative number"를 출력합니다. 
그 외의 경우 "Zero"를 출력합니다.

##### 스위치 표현식에서의 `when`

```csharp
int number = 10;

string result = number switch
{
    int n when n > 0 => "Positive number",
    int n when n < 0 => "Negative number",
    _ => "Zero"
};

Console.WriteLine(result); // 출력: Positive number
```

스위치 표현식에서도 `when` 키워드를 사용하여 
조건부 논리를 적용할 수 있습니다. 

##### 객체 패턴 매칭과 `when`

```csharp
public class Person
{
    public string Name { get; set; }
    public int Age { get; set; }
}

Person person = new Person { Name = "John", Age = 30 };

string description = person switch
{
    { Age: int age } when age >= 18 => $"{person.Name} is an adult.",
    { Age: int age } when age < 18 => $"{person.Name} is a minor.",
    _ => "Unknown age"
};

Console.WriteLine(description); // 출력: John is an adult.
```

이 예제에서는 `Person` 객체의 `Age` 속성을 검사하여, 성인인지 미성년자인지 구별합니다.

### 요약

#### `when` 키워드의 주요 기능
1. **조건부 논리 추가**: 특정 조건을 만족하는 경우에만 해당 케이스가 실행되도록 합니다.
2. **스위치 문과 스위치 표현식에서 사용**: 다양한 패턴 매칭과 결합하여 복잡한 조건을 처리할 수 있습니다.

#### 예제
1. **숫자 검사**: 숫자가 양수, 음수, 또는 0인지 구별.
2. **객체 검사**: 객체의 속성을 검사하여 조건에 따라 다른 로직 실행.

Q1:
`when` 키워드를 사용할 때, 조건이 복잡해지면 어떤 점에 주의해야 하나요?

Q2:
패턴 매칭과 `when` 키워드를 사용하여 실생활의 복잡한 비즈니스 로직을 어떻게 간단하게 구현할 수 있을까요?
---
title: 델리게이트 in CSharp
created: 2024-05-17 02:31
alias: [델리게이트]
tags:
---
#### 정의
델리게이트는 메서드의 참조를 저장하고 호출할 수 있는 타입입니다. 
메서드 시그니처를 정의하고, 
해당 시그니처와 일치하는 메서드를 참조할 수 있습니다.

#### 역할
- 메서드 참조 저장
- 일치하는 시그니처의 메서드 호출
- 멀티캐스트 가능 (여러 메서드를 참조 가능)

#### 예제

```csharp
// 델리게이트 선언
public delegate void MyDelegate(string message);

public class Example
{
    public void Method1(string message)
    {
        Console.WriteLine("Method1: " + message);
    }

    public void Method2(string message)
    {
        Console.WriteLine("Method2: " + message);
    }

    public void Execute()
    {
        MyDelegate del = Method1;
        del += Method2;

        // 델리게이트 호출
        del("Hello, World!");
    }
}
```

#### 특징
델리게이트는 호출자가 누구인지 알지 못합니다.
델리게이트는 직접적으로 호출할 수 있습니다.
델리게이트는 메서드 참조 목록을 유지하며, 등록된 모든 메서드를 호출할 수 있습니다.

---
title: CSharp 이벤트를 직접 구현
created: 2024-04-16 11:23
alias:
tags:
---
이벤트는 
객체나 클래스가 특정 작업을 수행할 때 
다른 객체에 알릴 수 있는 방법을 제공합니다. 

이벤트를 직접 구현하려면 몇 가지 주요 단계를 따라야 합니다.

### 1. 이벤트 정의

먼저, 이벤트를 발생시킬 클래스 내에 이벤트를 정의해야 합니다. 
이벤트는 일반적으로 대리자(delegate) 타입을 사용하여 정의됩니다. 

대리자는 메서드를 참조하는 타입으로, 
이벤트 처리기의 서명(즉, 메서드가 받아들이는 매개변수와 반환 타입)을 정의합니다.

```csharp
public class MyEventArgs : EventArgs
{
    public string Message { get; set; }
}

public delegate void MyEventHandler(object sender, MyEventArgs e);

public class Publisher
{
    // 이벤트 선언
    public event MyEventHandler MyEvent;

    protected virtual void OnMyEvent(MyEventArgs e)
    {
        MyEventHandler handler = MyEvent;
        handler?.Invoke(this, e);
    }

    public void DoSomething()
    {
        // 어떤 로직 수행
        OnMyEvent(new MyEventArgs { Message = "Event Triggered!" });
    }
}
```

### 2. 이벤트 구독

다음으로, 이벤트를 구독할 클래스나 메서드를 작성해야 합니다. 
이벤트를 구독한다는 것은, 
이벤트가 발생할 때 
호출될 메서드를 지정한다는 의미입니다.

```csharp
public class Subscriber
{
    public void OnMyEvent(object sender, MyEventArgs e)
    {
        Console.WriteLine($"Received message: {e.Message}");
    }
}
```

### 3. 이벤트 연결 및 실행

마지막으로, 
이벤트 발행자의 인스턴스를 생성하고, 
구독자의 메서드를 이벤트에 연결한 후, 
이벤트를 발생시키는 메서드를 호출합니다.

```csharp
Publisher publisher = new Publisher();
Subscriber subscriber = new Subscriber();

// 이벤트 구독
publisher.MyEvent += subscriber.OnMyEvent;

// 이벤트를 발생시키는 메서드 호출
publisher.DoSomething();
```

이벤트 구현의 이러한 방식은 
코드 내에서 비동기적으로 메시지를 전달하거나, 
특정 액션에 대한 반응으로 추가 작업을 수행하는 데 매우 유용합니다.

###### 이벤트 정의 및 선언
이벤트는 
대리자를 사용하여 
클래스 내에서 정의하며, 
이벤트를 발생시킬 때 호출될 메서드의 서명을 결정합니다.

###### 이벤트 구독 및 처리기 연결
다른 클래스나 메서드에서 이벤트를 구독하여, 
이벤트 발생 시 실행할 로직을 정의합니다.

###### 이벤트 발생
이벤트 발생 메서드 내에서 이벤트를 트리거하여 구독자에게 알립니다.



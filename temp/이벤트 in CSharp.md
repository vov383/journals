---
title: 이벤트 in CSharp
created: 2024-05-17 02:31
alias:
tags:
---
#### 정의
이벤트는 델리게이트를 기반으로 하며, 클래스 외부에서 델리게이트를 직접 호출하지 못하도록 제한합니다. 주로 객체 간의 통신을 위해 사용됩니다.

#### 역할
- 델리게이트를 사용하여 이벤트 핸들러를 등록
- 클래스 외부에서 이벤트를 호출하지 못하도록 보호
- 특정 동작(이벤트)이 발생했을 때 등록된 메서드(핸들러) 호출

#### 예제

```csharp
public class Publisher
{
    // 이벤트 선언
    public event EventHandler<MyEventArgs> MyEvent;

    protected virtual void OnMyEvent(MyEventArgs e)
    {
        MyEvent?.Invoke(this, e);
    }

    public void TriggerEvent()
    {
        OnMyEvent(new MyEventArgs("Hello, World!"));
    }
}

public class Subscriber
{
    public void Subscribe(Publisher publisher)
    {
        publisher.MyEvent += HandleEvent;
    }

    private void HandleEvent(object sender, MyEventArgs e)
    {
        Console.WriteLine("Event received: " + e.Message);
    }
}

public class MyEventArgs : EventArgs
{
    public string Message { get; }

    public MyEventArgs(string message)
    {
        Message = message;
    }
}
```

#### 특징
- 이벤트는 델리게이트를 기반으로 하지만, 클래스 외부에서 이벤트를 직접 호출할 수 없습니다.
- 이벤트는 주로 객체 간의 통신을 위해 사용됩니다.
- 이벤트는 보호 수준을 통해 이벤트가 클래스 내부에서만 발생하도록 제한합니다.



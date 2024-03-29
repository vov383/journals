---
title: SerializationInfo의 사용 방법 예시
created: 2024-03-29 12:25
alias:
tags:
---
.NET에서 클래스의 직렬화를 지원하려면, 
해당 클래스는 `ISerializable` 인터페이스를 구현해야 합니다. 
이 인터페이스에는 `GetObjectData` 메서드가 포함되어 있으며, 
이 메서드 내에서 
객체의 상태를 
`SerializationInfo` 객체에 저장하는 로직을 구현합니다.

```csharp
[Serializable]
public class ExampleClass : ISerializable
{
    public int Property1 { get; set; }
    public string Property2 { get; set; }

    // 이 생성자는 역직렬화 시 호출됩니다.
    protected ExampleClass(SerializationInfo info, StreamingContext context)
    {
        Property1 = info.GetInt32("Property1");
        Property2 = info.GetString("Property2");
    }

    // ISerializable 인터페이스 구현
    public void GetObjectData(SerializationInfo info, StreamingContext context)
    {
        info.AddValue("Property1", Property1);
        info.AddValue("Property2", Property2);
    }
}
```



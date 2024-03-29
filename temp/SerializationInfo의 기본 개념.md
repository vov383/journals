---
title: SerializationInfo의 기본 개념
created: 2024-03-29 12:24
alias:
tags:
---
###### 데이터의 저장과 복원
`SerializationInfo` 객체는 
직렬화할 객체의 데이터(상태)를 
키-값 쌍의 형태로 저장합니다. 
이 정보는 나중에 객체를 다시 생성할 때, 
즉 역직렬화할 때 사용됩니다.
###### 유연성
객체의 내부 구조가 변경되더라도, 
`SerializationInfo`를 사용함으로써 호환성을 유지할 수 있습니다. 
예를 들어, 클래스에 새로운 필드가 추가되더라도 
이전 버전의 직렬화된 데이터로부터 객체를 복원할 수 있습니다.
###### 보안
`SerializationInfo`는 
보안 상의 이유로 중요한 데이터를 직렬화 과정에서 제외시키거나, 
특정 조건 하에서만 데이터를 추가하는 등의 제어가 가능합니다.

#### SerializationInfo의 사용 방법 예시
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

#### 요약
###### SerializationInfo 개념
객체의 상태를 키-값 쌍으로 저장하여 
직렬화와 역직렬화를 지원하는 .NET 클래스입니다.
###### 기능과 이점
객체의 상태를 안전하게 저장하고 복원할 수 있으며, 
객체의 버전 관리와 호환성 유지에 유용합니다.
###### 사용법 
`ISerializable` 인터페이스를 구현하여 
객체의 상태를 `SerializationInfo`에 저장하고, 
역직렬화 시 이 정보를 사용하여 객체를 복원합니다.

이 개념은 데이터를 안전하게 저장하고, 
네트워크를 통해 전송하거나, 
파일 시스템에 저장할 때 중요합니다. 
또한, 애플리케이션의 다양한 버전 간의 호환성을 유지하는 데에도 필수적인 역할을 합니다.

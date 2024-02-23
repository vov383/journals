---
title: csharp property
created: 2024-02-23 10:21
alias:
tags:
---
C#에서 `public string Name { get; set; }` 형태로 사용되는 것은 프로퍼티(Property)라고 부르며, Java의 getter와 setter 메소드에 해당하는 기능을 제공합니다. 
C# 프로퍼티는 필드(클래스의 변수)에 대한 접근을 제어하는 방법을 간결하게 제공하며, 이를 통해 필드 값의 읽기(Getter)와 쓰기(Setter)를 위한 코드를 자동으로 생성할 수 있습니다.

# C# 프로퍼티 구성

C#에서 프로퍼티는 다음과 같이 구성됩니다:

- `get` 액세서: 이 부분은 프로퍼티 값을 읽을 때 실행되는 코드를 정의합니다. Java의 getter 메소드와 유사한 역할을 합니다.
- `set` 액세서: 이 부분은 프로퍼티에 값을 할당할 때 실행되는 코드를 정의합니다. Java의 setter 메소드와 유사한 역할을 수행합니다. `set` 액세서 내에서는 `value` 키워드를 사용하여 할당하려는 값을 참조할 수 있습니다.

# 예시

C#:
```csharp
public class Animal
{
    public string Name { get; set; }
}
```

Java:
```java
public class Animal {
    private String name;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }
}
```

C#의 프로퍼티는 Java에서 별도로 구현해야 하는 getter와 setter 메소드를 한 줄의 코드로 간소화할 수 있어 코드를 더 깔끔하게 유지하는 데 도움이 됩니다. 또한, C#에서는 프로퍼티의 `get`과 `set` 접근자에 추가 로직을 구현하여, 프로퍼티의 값을 읽거나 쓸 때 추가적인 작업을 수행할 수도 있습니다. 이러한 기능은 Java의 getter와 setter 메소드에서도 구현할 수 있지만, C#의 프로퍼티는 이를 더욱 간결하게 표현할 수 있습니다.



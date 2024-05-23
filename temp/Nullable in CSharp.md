---
title: Nullable in CSharp
created: 2024-05-23 08:00
alias:
tags:
---
#### 1. `?` (Nullable 형식)
C#에서 `?`는 nullable 형식을 나타내는 데 사용됩니다. 
이는 해당 변수에 null 값을 할당할 수 있게 해줍니다. 
주로 값 형식(value type)에서 사용됩니다.

예를 들어:
```csharp
int? nullableInt = null;
nullableInt = 5;
```

위의 코드에서 `int?`는 `Nullable<int>`를 의미합니다. 
즉, `nullableInt`는 정수값이나 `null`을 가질 수 있습니다.



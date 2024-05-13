---
title: DataRow의 Field
created: 2024-05-Su 23:19:30
aliases: 
tags:
---
`DataRow`의 `Field<T>()` 메소드를 사용하면 
타입을 명시적으로 지정하여 필드 값을 안전하게 읽을 수 있습니다. 
이 메소드는 내부적으로 타입 검사와 `DBNull` 처리를 수행하므로, 데이터 접근 코드를 더 간결하고 안전하게 작성할 수 있습니다.

**예시:**
```csharp
public EmployeeDTO ConvertDataRowToDTO(DataRow row)
{
    return new EmployeeDTO
    {
        EmployeeId = row.Field<int>("EmployeeId"),
        FirstName = row.Field<string>("FirstName"),
        LastName = row.Field<string>("LastName"),
        HireDate = row.Field<DateTime?>("HireDate")
    };
}
```
위 코드에서 `Field<T>()` 메소드를 사용하여 
각 필드 값을 직접 타입에 맞게 안전하게 읽습니다. 
`HireDate` 필드처럼 nullable 타입이 필요한 경우, 
`DateTime?`와 같이 nullable 형식을 지정할 수 있습니다. 
이 방법은 타입 안전성을 보장하며, 
`DBNull` 처리도 자동으로 수행합니다.
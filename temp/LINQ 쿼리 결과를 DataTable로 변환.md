---
title: LINQ 쿼리 결과를 DataTable로 변환
created: 2024-03-25 12:48
alias:
tags:
---
LINQ 쿼리의 결과를 다시 `DataTable`로 변환하고 싶다면, `CopyToDataTable` 메서드를 사용할 수 있습니다.
###### CopyToDataTable()
![[journals/temp/CopyToDataTable()]]


```csharp
var filteredRows = dataSet.Tables["People"].AsEnumerable()
    .Where(row => row.Field<int>("Age") >= 30)
    .CopyToDataTable();
```


###### CopyToDataTable() 비어 있는 예외 처리

`CopyToDataTable` 메서드는 LINQ 쿼리의 결과를 `DataTable`로 변환하는 데 사용됩니다. 그러나, 이 메서드는 쿼리 결과가 비어 있을 경우 `InvalidOperationException`을 발생시킵니다. 따라서 쿼리 결과가 비어 있는 경우를 적절히 처리하는 것이 중요합니다.

###### 예외 처리 방법

**결과 검사**
쿼리 실행 전에 결과가 비어 있는지 여부를 검사합니다. 
예를 들어, `Any()` 메서드를 사용하여 결과 집합에 적어도 하나의 요소가 있는지 확인할 수 있습니다. 
결과가 있을 경우에만 `CopyToDataTable`을 호출합니다.
   
**확장 메서드 생성**
쿼리 결과가 비어 있을 때 빈 `DataTable`을 반환하는 사용자 정의 확장 메서드를 생성할 수 있습니다. 
이 방법은 `CopyToDataTable` 메서드의 기능을 확장하여, 결과 집합이 비어 있을 때 예외를 피할 수 있게 합니다.

###### 확장 메서드 예제

아래는 쿼리 결과가 비어 있을 경우 빈 `DataTable`을 반환하는 사용자 정의 확장 메서드의 예제입니다.

```csharp
public static class LinqExtensions
{
    public static DataTable CopyToDataTableOrEmpty<T>(this IEnumerable<T> source, DataTable dataTable) where T : DataRow
    {
        if (source.Any())
        {
            return source.CopyToDataTable();
        }
        else
        {
            return dataTable.Clone(); // 같은 스키마의 빈 DataTable 반환
        }
    }
}
```

이 확장 메서드를 사용하면, 쿼리 결과가 비어 있을 때 빈 `DataTable`을 쉽게 생성할 수 있습니다.

```csharp
DataTable result = dataSet.Tables["People"].AsEnumerable()
    .Where(row => row.Field<int>("Age") > 100) // 예시로, 결과가 없을 조건
    .CopyToDataTableOrEmpty(dataSet.Tables["People"]);
```

이 방법은 `CopyToDataTable` 메서드의 사용성을 개선하며, 결과가 비어 있을 경우에 대한 예외를 방지합니다.

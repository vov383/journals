---
title: LINQ의 `SequenceEqual`과 `DataRowComparer.Default` 동작 방법
created: 2024-08-21 05:14
alias:
tags:
---
#### `SequenceEqual`의 동작 방식

`SequenceEqual`은 LINQ에서 제공하는 메서드로, 두 컬렉션이 순서대로 동일한지 비교합니다. 이 메서드는 다음과 같은 방식으로 작동합니다:

1. **동일한 크기 비교**: 두 컬렉션의 요소 수가 같지 않으면 `false`를 반환합니다.
2. **순차적 비교**: 각 컬렉션의 요소를 첫 번째 요소부터 마지막 요소까지 순차적으로 비교합니다.
3. **모든 요소가 동일할 때**: 두 컬렉션의 모든 요소가 순서대로 동일하면 `true`를 반환하고, 하나라도 다르면 `false`를 반환합니다.

위 예제에서 `dt1Rows.SequenceEqual(dt2Rows, DataRowComparer.Default)`는 `dt1Rows`와 `dt2Rows`의 각 행이 같은 순서로 동일한지 비교합니다. 

#### `DataRowComparer.Default`의 역할

`DataRowComparer.Default`는 `DataRow` 객체를 비교하기 위한 기본 비교기를 제공합니다. `DataRowComparer`는 기본적으로 `DataRow`의 모든 열 값이 같은지 비교하며, 다음과 같은 방식으로 작동합니다:

1. **행 비교**: 각 `DataRow`의 모든 열 데이터를 순차적으로 비교합니다.
2. **모든 열이 동일할 때**: 두 행의 모든 열 값이 동일하면 두 `DataRow`는 동일하다고 간주됩니다.
3. **하나라도 다른 열이 있을 때**: 두 행의 열 값 중 하나라도 다르면 두 `DataRow`는 다르다고 간주됩니다.

#### 예제

이 예제에서 `SequenceEqual`과 `DataRowComparer.Default`가 어떻게 동작하는지 이해할 수 있습니다.

```csharp
using System;
using System.Data;
using System.Linq;

public class Program
{
    public static void Main()
    {
        // 첫 번째 DataTable 생성 및 데이터 추가
        DataTable dt1 = new DataTable();
        dt1.Columns.Add("ID", typeof(int));
        dt1.Columns.Add("Name", typeof(string));
        dt1.Rows.Add(1, "John");
        dt1.Rows.Add(2, "Jane");

        // 두 번째 DataTable 생성 및 데이터 추가
        DataTable dt2 = new DataTable();
        dt2.Columns.Add("ID", typeof(int));
        dt2.Columns.Add("Name", typeof(string));
        dt2.Rows.Add(1, "John");
        dt2.Rows.Add(2, "Jane");

        // 두 DataTable의 행을 비교
        var dt1Rows = dt1.AsEnumerable();
        var dt2Rows = dt2.AsEnumerable();

        bool areEqual = dt1Rows.SequenceEqual(dt2Rows, DataRowComparer.Default);

        Console.WriteLine("DataTables are equal: " + areEqual);
    }
}
```

이 예제에서 `areEqual` 변수는 `true`를 반환합니다. 이는 두 `DataTable`이 순서대로 동일한 행을 가지고 있기 때문입니다.

#### 요약

h6 `SequenceEqual` 설명
두 컬렉션의 요소를 순서대로 비교하여 동일하면 `true`를 반환합니다.

h6 `DataRowComparer.Default` 설명
`DataRowComparer.Default`는 `DataRow` 객체를 비교하기 위한 기본 비교기이며, 모든 열이 동일한지 확인합니다.

h6 동작 원리
`SequenceEqual`은 각 `DataRow`를 `DataRowComparer.Default`를 통해 비교하며, 모든 행이 동일한 순서로 일치할 때 `true`를 반환합니다.

Q1: `DataRowComparer.Default` 대신 커스텀 비교기를 사용하려면 어떻게 구현할 수 있을까요?
Q2: `SequenceEqual`과 `DataRowComparer.Default`를 사용해 대규모 데이터셋을 비교할 때 성능을 개선하는 방법은 무엇일까요?



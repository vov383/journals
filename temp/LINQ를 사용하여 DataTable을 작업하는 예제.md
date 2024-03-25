---
title: LINQ를 사용하여 DataTable을 작업하는 예제
created: 2024-03-25 01:36
alias:
tags:
---
###### DataSet과 DataTable 준비
먼저, LINQ 쿼리를 실행할 DataSet과 DataTable을 준비합니다. 
예를 들어, DataTable에는 'ID', 'Name', 'Age' 열이 있다고 가정합니다.

###### LINQ 쿼리 사용
DataTable에 대한 LINQ 쿼리를 작성하여 특정 조건을 만족하는 행을 검색합니다. 
예를 들어, 'Age'가 30 이상인 모든 행을 찾는 쿼리를 작성할 수 있습니다.

###### 쿼리 결과 처리
쿼리의 결과를 반복 처리하여 필요한 작업을 수행합니다. 
예를 들어, 검색된 행의 정보를 출력할 수 있습니다.

###### 예제 코드
아래 예제 코드는 위에서 설명한 과정을 구현한 것입니다. DataSet 내의 DataTable에서 'Age' 열이 30 이상인 행을 선택하고, 그 결과를 출력합니다.

```csharp
using System;
using System.Data;
using System.Linq;

class Program
{
    static void Main()
    {
        // DataSet과 DataTable 생성 및 초기화
        DataSet dataSet = new DataSet();
        DataTable table = new DataTable("People");
        table.Columns.Add("ID", typeof(int));
        table.Columns.Add("Name", typeof(string));
        table.Columns.Add("Age", typeof(int));
        table.Rows.Add(1, "John Doe", 28);
        table.Rows.Add(2, "Jane Doe", 32);
        table.Rows.Add(3, "Mike Johnson", 40);
        dataSet.Tables.Add(table);

        // LINQ 쿼리로 'Age'가 30 이상인 행 선택
        var query = from row in dataSet.Tables["People"].AsEnumerable()
                    where row.Field<int>("Age") >= 30
                    select row;

        // 쿼리 결과 출력
        foreach (var row in query)
        {
            Console.WriteLine($"ID: {row["ID"]}, Name: {row["Name"]}, Age: {row["Age"]}");
        }
    }
}
```

###### 실행 결과
이 코드를 실행하면 'Age' 열의 값이 30 이상인 행의 정보를 출력합니다.

Q1 : LINQ를 사용하여 다른 조건(예: 이름이 'John Doe'인 사람 찾기)으로 DataTable을 쿼리하는 방법은 무엇인가요?
Q2 : LINQ 쿼리 결과를 DataTable로 변환하는 방법은 무엇인가요?


###### AsEnumerable()
![[journals/temp/AsEnumerable()]]


###### LINQ 쿼리 결과를 DataTable로 변환
![[journals/temp/LINQ 쿼리 결과를 DataTable로 변환]]


이 코드 조각은 'Age'가 30 이상인 행만을 필터링하고, 그 결과를 새 `DataTable` 객체에 담습니다.

Q2 : `CopyToDataTable` 메서드 사용 시 결과가 비어 있는 경우에 대한 예외 처리는 어떻게 하나요?


Q1 : 사용자 정의 확장 메서드를 생성할 때 고려해야 할 다른 유용한 기능은 무엇이 있을까요?
Q2 : LINQ와 `DataTable`을 사용할 때 성능을 최적화하는 전략에는 어떤 것들이 있을까요?



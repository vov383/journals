---
title: AsEnumerable()
created: 2024-03-25 12:47
alias:
tags:
---
`AsEnumerable()` 메서드는 `DataTable`의 행 컬렉션을 `IEnumerable<DataRow>` 타입으로 변환합니다. 
이 변환을 통해 LINQ 쿼리를 `DataTable`에 적용할 수 있게 됩니다. 
기본적으로, `DataTable`의 `Rows` 속성은 `DataRowCollection` 타입으로, LINQ 쿼리를 직접 사용할 수 없습니다.
`AsEnumerable()` 메서드를 사용함으로써, LINQ의 강력한 쿼리 기능을 `DataTable`에 적용할 수 있는 길이 열립니다.

###### AsEnumerable()의 사용
`AsEnumerable()` 메서드를 호출하면 
`DataTable`의 각 행에 대해 반복하거나, 
조건에 맞는 행을 필터링하거나, 
행 데이터를 선택적으로 추출하는 등의 작업을 LINQ 쿼리를 통해 수행할 수 있습니다. 
이는 데이터 처리를 더 유연하고 간결하게 만들어 줍니다.

###### 예제를 통한 이해
위에서 제시한 예제에서 `dataSet.Tables["People"].AsEnumerable()` 구문을 통해, 
'People' `DataTable`의 행들을 `IEnumerable<DataRow>`로 변환하여, 
`where` 절을 사용한 필터링 같은 LINQ 쿼리 작업을 가능하게 합니다.



---
title: dataGridView에 데이터를 표시하는 두 가지 방식
created: 2024-02-23 03:43
alias:
tags:
---
`DataGridView`에 데이터를 표시하는 두 가지 방식에는 각각 장단점이 있습니다. 아래에서는 `DataSource` 속성을 사용하는 방법과 수동으로 행을 추가하는 방법을 비교합니다.

###### DataSource 속성 사용
![[DataSource 속성 사용]]


# 수동으로 행 추가

```csharp
foreach (DataRow row in dt.Rows) 
{
    // 조건에 따른 데이터 변환 및 추가
    dataGridView1.Rows.Add(/* 변환된 데이터 */);
}
```

**장점:**
- **유연성**: 데이터를 `DataGridView`에 추가하기 전에, 데이터 변환, 조건 검사, 포맷 변경 등의 작업을 수행할 수 있어 매우 유연합니다.
- **커스터마이징**: 특정 로우나 셀에 대해 세밀한 스타일 적용이나 조건부 로직을 구현하기 쉽습니다.

**단점:**
- **코드 복잡도**: 각 행을 수동으로 추가하려면 더 많은 코드가 필요하며, 데이터 소스의 구조가 변경될 경우 해당 코드를 수정해야 할 수도 있습니다.
- **성능**: 대량의 데이터를 수동으로 처리할 때 성능 저하가 발생할 수 있습니다. 특히, `Rows.Add` 메서드를 반복적으로 호출하면서 많은 양의 데이터를 추가할 때 더욱 그렇습니다.
- **유지보수**: 데이터 소스의 구조나 요구사항이 변경될 경우, 이를 반영하기 위해 관련 코드를 찾아 수정해야 합니다.

# 결론

- 데이터를 단순히 표시하기만 하는 경우, `DataSource` 속성을 사용하는 것이 더 효율적입니다.
- 데이터에 대한 세밀한 제어나 조건부 로직이 필요한 경우, 수동으로 행을 추가하는 방식이 더 적합할 수 있습니다.
- 대량의 데이터를 다루는 경우, 성능을 고려하여 적절한 방법을 선택해야 합니다.
- 가능하다면, `DataGridView`의 커스텀 셀 및 로우 스타일링 기능, 이벤트 처리 기능 등을 활용하여 `DataSource` 방식의 유연성을 높이는 방법도 고려해 볼 수 있습니다.



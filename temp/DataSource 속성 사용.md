---
title: DataSource 속성 사용
created: 2024-02-23 04:08
alias:
tags:
---
```csharp
dataGridView1.DataSource = table;
```

**장점:**
- **간결함**: 단 한 줄의 코드로 `DataGridView`를 데이터와 바인딩할 수 있어 코드가 매우 간결해집니다.
- **자동 업데이트**: `DataSource`에 바인딩된 데이터가 변경될 때 `DataGridView`가 자동으로 업데이트됩니다.
- **쉬운 데이터 관리**: 데이터 조작(추가, 수정, 삭제)이 `DataTable` 또는 `List` 등에서 직접 이루어질 수 있으며, 이러한 변경사항이 자동으로 `DataGridView`에 반영됩니다.
- **성능**: 대량의 데이터를 다룰 때, `DataSource` 방식은 더 나은 성능을 제공할 수 있습니다.

**단점:**
- **유연성 부족**: `DataGridView`의 각 셀에 대한 세밀한 제어가 어렵습니다. 예를 들어, 특정 조건에 따라 셀의 값을 변환하거나 포맷을 변경하기 어렵습니다.

###### DataSource 속성 유연하게 사용하기
![[DataSource 속성 유연하게 사용하기]]



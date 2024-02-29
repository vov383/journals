---
title: DataGridView 속성
created: 2024-02-23 04:55
alias:
tags:
---
# DataSource
###### 테이블 매핑할 때 데이터 소스 속성 사용

# AutoGenerateColumns
자동 생성 컬럼
`DataGridView`의 `AutoGenerateColumns` 속성이 `true`로 설정되어 있으면, 바인딩된 데이터 소스의 모든 필드에 대한 컬럼을 자동으로 생성합니다. 
만약 데이터 소스에 빈 필드나 예상치 못한 추가 필드가 포함되어 있다면, 이로 인해 빈 컬럼이 생길 수 있습니다.

# RowHeader

# AutoSizeColumnsMode

# Columns
개별 컬럼을 다룰 때 사용함
## 컬럼 헤더 텍스트 변경
## 컬럼 표시 유무 변경
## 컬럼 표시 순서 변경

```csharp
dataGridView객체명.Columns["특정컬럼명"].HeaderText = "str"; // 컬럼 헤더텍스트 변경

dataGridView1.Columns["id"].Visible = false; // 컬럼 표시유무 변경

dataGridView1.Columns["emp_name"].DisplayIndex = 0; // 컬럼 표시 순서 변경
dataGridView1.Columns["department"].DisplayIndex = 1;
```

## 특정 컬럼의 셀 데이터 변경
### CellFormatting 이벤트
```csharp
dataGridView1.Columns[e.ColumnIndex].Name == "gender"
```

# SelectionMode
셀 셀렉트 - 개별 셀 선택
풀 로우 - row 하나 전체 선택
풀 컬럼 - 
로우 헤더
컬럼 헤더

## SelectionMode 선택기준
### 사용자 요구 사항 이해: 
사용자가 가장 자주 수행해야 하는 작업에 따라 선택 모드를 선택합니다. 예를 들어, 사용자가 전체 레코드를 자주 편집하는 경우 FullRowSelect가 가장 사용자 친화적인 옵션일 수 있습니다.

### 성능에 미치는 영향: 
성능과 사용자 경험에 미치는 영향을 염두에 두세요. 데이터 사용량이 많은 애플리케이션에서는 행이나 열을 많이 선택하면 리소스가 많이 소모될 수 있습니다.

### 유용성을 위한 사용자 정의: 
때로는 기본 동작이 정확히 필요한 동작이 아닐 수도 있습니다. CellClick과 같은 이벤트를 처리하여 프로그래밍 방식으로 선택을 제어하고 애플리케이션 요구 사항에 따라 다양한 동작을 제공할 수 있습니다.



[[DataSource 속성 사용]]
[[dotnet DataGridView]]
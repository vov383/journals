---
title: dotnet 윈폼 table에서 셀 선택하기.
created: 2024-02-22 12:42
alias:
tags:
---
# 1. 셀 선택 가능 여부 설정

`DataGridView` 컨트롤에서는 특정 셀이나 행, 열의 선택 가능 여부를 설정할 수 있습니다. 만약 `SelectionMode` 속성이 `FullRowSelect`, `RowHeaderSelect`와 같이 설정되어 있으면, 사용자가 특정 셀을 선택하는 것이 아니라 행 전체 또는 행 헤더를 선택하게 됩니다. 또한, `ReadOnly` 속성이 `true`로 설정된 경우, 셀을 클릭해도 편집이 불가능하므로 클릭이 제한적으로 느껴질 수 있습니다.


```cs
dataGridView1.SelectionMode = DataGridViewSelectionMode.FullRowSelect; dataGridView1.ReadOnly = true; // 이 경우, 셀을 클릭해도 편집이 안됩니다.`
```

# 2. 셀 클릭 이벤트 핸들러

셀 클릭 이벤트(`CellClick` 이벤트)의 핸들러에서 특정 조건에 따라 다르게 동작하도록 구현된 경우, 예를 들어 특정 컬럼(`id` 컬럼)의 셀만 클릭 이벤트를 처리하고 나머지 셀 클릭은 무시하도록 설정할 수 있습니다. 이는 클릭 이벤트 내에서 현재 클릭된 셀의 위치를 확인하고 그에 따라 다른 동작을 수행하게 하는 로직으로 구현됩니다.

```cs
private void dataGridView1_CellClick(object sender, DataGridViewCellEventArgs e) 
{     
	// id 컬럼만 처리하도록 설정     
	if (e.ColumnIndex == dataGridView1.Columns["id"].Index)    
	 {         
		 // id 컬럼 클릭 시의 동작     
	 }     
	 else     
	 {         
		 // 나머지 셀 클릭은 처리하지 않음     
	 } 
}
```

# 3. 셀의 `ReadOnly` 속성 설정

`DataGridView`의 각 셀마다 `ReadOnly` 속성을 개별적으로 설정할 수 있습니다. 특정 셀이나 열을 읽기 전용으로 설정하면, 해당 셀이나 열은 클릭이 가능하더라도 데이터의 수정은 불가능하게 됩니다. 사용자가 셀을 클릭할 때 명확한 시각적 피드백(예: 편집 가능한 셀의 테두리 색상 변경)이 없다면, 셀 클릭이 제대로 작동하지 않는 것처럼 느껴질 수 있습니다.

```cs
// 특정 열을 읽기 전용으로 설정
dataGridView1.Columns["id"].ReadOnly = true;

// 나머지 열은 읽기 전용으로 설정하지 않음
foreach (DataGridViewColumn column in dataGridView1.Columns)
{
    if (column.Name != "id")
    {
        column.ReadOnly = false;
    }
}

```

이러한 설정들은 사용자 인터페이스의 동작을 제어하기 위해 필요할 수 있지만, 사용자가 예상하는 동작과 다를 경우 혼란을 줄 수 있습니다. 따라서 이벤트 핸들러 또는 컨트롤의 속성 설정을 재검토하여 원하는 동작을 정확히 구현하는 것이 중요합니다.

문제 해결을 위해 다음 단계를 시도해 보세요:


---
title: LINQ GroupBy()로 컬랙션을 그룹으로 나누기
created: 2024-05-23 08:03
alias:
tags:
---
한 번의 LINQ 쿼리로 `MOVE` 값의 존재 여부와 `MAKETYPE` 값에 따라 데이터를 네 개의 그룹으로 나누기 위해서는, 
`GroupBy`를 두 개의 조건으로 사용할 수 있습니다. 

아래는 그 예제 코드입니다:

```csharp
var groupedLists = ds.Tables[0]
    .AsEnumerable()
    .GroupBy(row => new 
    { 
        IsMoveEmpty = string.IsNullOrEmpty($"{row["MOVE"]}"), 
        MakeType = $"{row["MAKETYPE"]}" 
    })
    .Select(g => new
    {
        g.Key.IsMoveEmpty,
        g.Key.MakeType,
        Rows = g.Select(row => row.Table.Columns
            .Cast<DataColumn>()
            .ToDictionary(
                col => col.ColumnName,
                col => row[col])
        )
        .OrderBy(row => row["DT_START"])
        .ToList()
    })
    .ToList();

var notMovedMakeType0 = groupedLists
    .FirstOrDefault(g => g.IsMoveEmpty == true && g.MakeType == "0")?.Rows ?? new List<Dictionary<string, object>>();

var notMovedMakeType1 = groupedLists
    .FirstOrDefault(g => g.IsMoveEmpty == true && g.MakeType == "1")?.Rows ?? new List<Dictionary<string, object>>();

var movedMakeType0 = groupedLists
    .FirstOrDefault(g => g.IsMoveEmpty == false && g.MakeType == "0")?.Rows ?? new List<Dictionary<string, object>>();

var movedMakeType1 = groupedLists
    .FirstOrDefault(g => g.IsMoveEmpty == false && g.MakeType == "1")?.Rows ?? new List<Dictionary<string, object>>();
```

### 코드 설명

1. **GroupBy**: `MOVE` 값의 존재 여부 (`IsMoveEmpty`)와 `MAKETYPE` 값 (`MakeType`)을 기준으로 데이터를 그룹화합니다.
2. **Select**: 각 그룹에 대해 딕셔너리 형태로 변환하고, `DT_START` 컬럼을 기준으로 정렬합니다.
3. **groupedLists**: 그룹화된 리스트를 저장합니다.
4. **notMovedMakeType0**: `MOVE`가 비어있고 `MAKETYPE`이 0인 그룹을 선택하여 리스트를 생성합니다.
5. **notMovedMakeType1**: `MOVE`가 비어있고 `MAKETYPE`이 1인 그룹을 선택하여 리스트를 생성합니다.
6. **movedMakeType0**: `MOVE`가 비어있지 않고 `MAKETYPE`이 0인 그룹을 선택하여 리스트를 생성합니다.
7. **movedMakeType1**: `MOVE`가 비어있지 않고 `MAKETYPE`이 1인 그룹을 선택하여 리스트를 생성합니다.

### 요약

1. `GroupBy`를 사용하여 `MOVE` 값의 존재 여부와 `MAKETYPE` 값에 따라 그룹화합니다.
2. 각 그룹을 딕셔너리 형태로 변환하고 정렬합니다.
3. 그룹화된 리스트에서 네 개의 하위 리스트를 추출합니다: `notMovedMakeType0`, `notMovedMakeType1`, `movedMakeType0`, `movedMakeType1`.

Q1: GroupBy를 사용하여 여러 조건으로 데이터를 그룹화할 때 주의해야 할 점은 무엇인가요?  
Q2: 데이터 그룹화 후 각 그룹을 처리할 때 발생할 수 있는 잠재적인 문제는 무엇인가요?



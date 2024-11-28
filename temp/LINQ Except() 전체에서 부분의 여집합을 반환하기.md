---
title: LINQ Except() 전체에서 부분의 여집합을 반환하기
created: 2024-11-28 04:31
alias:
tags:
---
`ulDtos`에서 `_ulDtosFiltered`에 없는 항목을 필터링하려면 LINQ의 `Except` 메서드 또는 키 기반 필터링을 사용할 수 있습니다. 아래는 두 가지 방법으로 구현한 예제입니다.

### 방법 1: LINQ `Except` 사용

```csharp
var notIn = ulDtos.Except(_ulDtosFiltered).ToList();
```

#### 설명

- `Except`는 기본적으로 참조 비교를 수행합니다. `UnloadPlanOrderDto` 객체의 참조가 다르면 같은 데이터를 가지더라도 다른 것으로 간주합니다.
- 객체 내용 기반 비교가 필요하다면 `UnloadPlanOrderDto`에 `Equals` 및 `GetHashCode`를 재정의해야 합니다.

#### 출력 예제

`notIn`에는 `_ulDtosFiltered`에 포함되지 않은 항목이 포함됩니다.

---

### 방법 2: 키 기반 비교

`UnloadPlanOrderDto`에 특정 키(예: ID)가 있다면 키 기반 필터링이 가능합니다.

```csharp
var filteredIds = new HashSet<string>(_ulDtosFiltered.Select(dto => dto.ID)); // ID를 기준으로 HashSet 생성

var notIn = ulDtos
    .Where(dto => !filteredIds.Contains(dto.ID))
    .ToList();
```

#### 설명

- `_ulDtosFiltered.Select(dto => dto.ID)`로 필터된 DTO의 키(ID)를 가져옵니다.
- `HashSet`은 빠른 검색을 제공하므로 성능이 좋습니다.
- `ulDtos`에서 `_ulDtosFiltered`의 키가 없는 항목만 필터링합니다.

#### 출력 예제

`notIn`에는 `_ulDtosFiltered`의 ID에 포함되지 않는 DTO가 포함됩니다.

---

### 방법 3: 커스텀 비교

객체의 특정 속성을 기준으로 필터링하려면 `IEqualityComparer`를 구현할 수도 있습니다.

```csharp
public class UnloadPlanOrderDtoComparer : IEqualityComparer<UnloadPlanOrderDto>
{
    public bool Equals(UnloadPlanOrderDto x, UnloadPlanOrderDto y)
    {
        return x.ID == y.ID; // ID로 비교
    }

    public int GetHashCode(UnloadPlanOrderDto obj)
    {
        return obj.ID.GetHashCode(); // ID의 해시코드 반환
    }
}

// 필터링
var comparer = new UnloadPlanOrderDtoComparer();
var notIn = ulDtos.Except(_ulDtosFiltered, comparer).ToList();
```

#### 설명

- `IEqualityComparer`를 통해 객체의 특정 속성(ID)만 비교하도록 설정합니다.
- `Except`에 커스텀 비교자를 전달합니다.

---

### 요약

1. 참조 비교는 `Except`를 바로 사용.
2. 키 기반 비교는 `HashSet` 활용.
3. 여러 속성을 비교하거나 커스텀 비교가 필요하면 `IEqualityComparer`를 구현.

Q1: 필터링 기준이 ID 외에 다른 속성(예: Name, Date 등)도 포함된다면 어떤 방식이 적합할까요?  
Q2: 성능 최적화를 위해 데이터 크기와 필터 조건에 따라 어떤 방법이 더 유리할까요?


